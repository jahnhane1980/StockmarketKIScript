# MISSION: Financial Macro-Handshake (V15 - Liquidity-Plug Edition)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten (Stichtag: 03.04.2026). 
Die Makro-Bewertung muss zwingend nach Asset-Typ (A/B) getrennt werden. Der Bitcoin-Kill-Switch hat absolute Priorität vor allen anderen Indikatoren.

---

## 0. INPUT INTERFACE
Das Skript verarbeitet Eingangsdaten in diesem Format:

{
  "analysis_request": {
    "tickers": [
      { "id": "NVDA", "status": "LONG" },
      { "id": "PLTR", "status": "LONG" },
      { "id": "NVTS", "status": "CASH" },
      { "id": "TTD", "status": "CASH" },
      { "id": "CRM", "status": "LONG" }
    ]
  }
}

---

## 1. PHASE 1: AUTO-CLASSIFICATION & REGIME
Identifiziere jeden Ticker automatisch:
- TYPE B (Mega-Cap): Marktkapitalisierung > $250 Mrd. (Fokus: Net-Liq, GEX, Institutional Prints).
- TYPE A (Growth): Marktkapitalisierung < $250 Mrd. (Fokus: BTC-Proxy, OBV-Divergenz).

Regime-Auswahl basierend auf 'status':
- status: LONG -> Aktiviere LOGIK-BLOCK A (EXIT-RADAR).
- status: CASH -> Aktiviere LOGIK-BLOCK B (ENTRY-HUNTER).

---

## 2. PHASE 2: SPLIT GLOBAL MACRO-SCORING
Berechne die Basis-Scores (S_NetLiq, S_BTC, S_Breadth) auf einer Skala von 0-10.

### A. Dynamische Gewichtung pro Typ
- Score für TYPE A (High-Beta): S_macro_A = (S_BTC * 0.7) + (S_NetLiq * 0.3)
- Score für TYPE B (Mega-Cap): S_macro_B = (S_BTC * 0.4) + (S_NetLiq * 0.4) + (S_Breadth * 0.2)

### B. Global Guards (Der Stecker-Zieher)
1. Penalty-Guard: Wenn BTC < 200-SMA ODER BTC-Monats-Performance < -20%: Addiere +3 Punkte auf alle S_macro Scores (Maximum 10.0).
2. Kill-Switch (Nur Type A): Wenn BTC-Monats-Performance < -30%: Setze S_final für alle Type A Ticker zwingend auf 10.0 (Status: HARD_EXIT).

---

## 3. LOGIK-BLOCK A: EXIT-RADAR (Nur für 'LONG')
Berechne das spezifische Risiko (S_micro von 0-10):
- SMA-Stretch: Preis > 35% über 200-Tage-Linie (+3 Punkte).
- GEX-Wall (Type B): Preis an Call-Wand + fallendes Gamma (+3 Punkte).
- BTC-Lag (Type A): Aktie fällt deutlich stärker als BTC (+2 Punkte).
- OBV-Distribution (Type A): Preis macht Higher High, OBV macht Lower High (+2 Punkte).

---

## 4. LOGIK-BLOCK B: ENTRY-HUNTER (Nur für 'CASH')
Prüfe Signale (Nur aktiv, wenn S_macro < 7.0):
- GEX-Flip (Type B): Wechsel von negativem zu positivem Gamma (Zwingend).
- OBV-Divergence (Type A): Bullish Divergence (Zwingend).
- Institutional Flow: Sichtbare Kauf-Prints in Dark Pools.
- Trend-Reclaim: Preis schließt über dem 20-Tage-SMA.

---

## 5. FINAL CALCULATION
S_final = (S_macro_[Typ] * 0.6) + (S_micro * 0.4)

Action Labels & Mapping:
- 1.0 - 4.5: "BULLISH / SCALE_IN" (Nur verfügbar für CASH-Status).
- 4.6 - 6.5: "NEUTRAL_WATCH" (Halten oder Beobachten).
- 6.6 - 8.5: "REDUCE_50_PERCENT" (Teilverkäufe).
- 8.6 - 10.0: "HARD_EXIT / CASH" (Vollständige Schließung).

---

## 6. OUTPUT-STRUKTUR
Das Ergebnis wird wie folgt ausgegeben:

{
  "timestamp": "ISO-Zeitstempel",
  "global_macro": { 
    "type_a_score": 0-10, 
    "type_b_score": 0-10, 
    "guards_active": ["Liste der aktiven Guards"] 
  },
  "tickers": [
    {
      "id": "TICKER",
      "type": "A/B",
      "final_score": 0-10,
      "action": "LABEL",
      "logic_notes": ["Details zu Triggern"]
    }
  ]
}

---

### // --- MANUELLE ÄNDERUNGSHINWEISE (V14 -> V15) ---
### // Änderung 1: Einführung einer getrennten Makro-Berechnung. Typ A (Growth) reagiert jetzt fast ausschließlich auf Liquidität (BTC), während Typ B (Mega-Caps) breiter gefasst bleibt.
### // Änderung 2: Bitcoin-Gewichtung für Typ A Aktien massiv erhöht (von ca. 33% auf 70%). Das verhindert, dass stabiles Makro einen Absturz bei Growth-Titeln maskiert.
### // Änderung 3: Einbau des "Kill-Switch". Bei einem Krypto-Absturz von >30% werden Growth-Titel ohne Wenn und Aber liquidiert.
### // Änderung 4: Der "Penalty-Guard" sorgt für eine pauschale Risiko-Erhöhung (+3), wenn Bitcoin unter seinem langfristigen Trend (200-SMA) notiert.
### // Änderung 5: Die Logik wurde so kalibriert, dass Blow-off-Tops bei High-Beta-Aktien durch die hohe BTC-Sensitivität früher erkannt werden.
### // --- ENDE DER DOKUMENTATION ---