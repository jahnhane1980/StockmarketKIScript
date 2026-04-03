# MISSION: Financial Macro-Handshake (V16 - Aggressive Cycle-Timer)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten (Stichtag: 03.04.2026). 
Die Bitcoin-Analyse fungiert als binärer Master-Switch für alle Asset-Typen. Jede Analyse beginnt zwingend mit der Bestimmung des BTC-Status.

---

## 0. INPUT INTERFACE
Das Skript verarbeitet die Eingangsdaten in diesem Format (JSON-String):

{ "analysis_request": { "btc_metrics": { "mvrv_z_score": 0.0, "production_cost": 80000, "hash_ribbons": "NEUTRAL", "pi_cycle_proximity": 0.95 }, "tickers": [ { "id": "NVDA", "status": "CASH" }, { "id": "PLTR", "status": "CASH" }, { "id": "NOW", "status": "CASH" }, { "id": "CRM", "status": "CASH" } ] } }

---

## 1. PHASE 1: BTC MASTER-SWITCH (Aggressive Calibration)
Bestimme den globalen btc_status (LONG oder CASH) basierend auf Zyklus-Extremen:

### A. Bottom-Finder (Aggressiv)
Setze btc_status = LONG, wenn EINER dieser Trigger aktiv ist:
1. MVRV-Frontrun: MVRV Z-Score < 0.2 (Beginn der tiefen Value-Zone).
2. Cost-Floor: Aktueller Preis < 110% der Produktionskosten (Mining-Capitulation Schutz).
3. RSI-Oversold: Weekly RSI < 35.

### B. Top-Finder (Aggressiv)
Setze btc_status = CASH, wenn EINER dieser Trigger aktiv ist:
1. Pi-Cycle Warning: Pi-Cycle Proximity > 0.98 (Vermeidung des finalen Blow-off Tops).
2. MVRV-Heat: MVRV Z-Score > 6.5 (Extreme Überhitzung).
3. Divergence-Kill: Preis macht Higher High, aber Daily RSI sinkt über 14 Tage (Momentum-Verlust).

---

## 2. PHASE 2: AUTO-CLASSIFICATION & WEIGHTING
Identifiziere Ticker-Typen automatisch:
- TYPE B (Mega-Cap): Marktkapitalisierung > $250 Mrd. (Fokus: Liquidität & GEX).
- TYPE A (Growth): Marktkapitalisierung < $250 Mrd. (Fokus: BTC-Proxy & OBV).

### Dynamische Makro-Scores ($S_{macro}$)
- Wenn btc_status == CASH: Addiere pauschal +4.0 auf alle $S_{macro}$ Scores (Veto-Effekt).
- Gewichtung TYPE A: $S_{macro\_A} = (S_{BTC} \cdot 0.7) + (S_{NetLiq} \cdot 0.3)$
- Gewichtung TYPE B: $S_{macro\_B} = (S_{BTC} \cdot 0.4) + (S_{NetLiq} \cdot 0.4) + (S_{Breadth} \cdot 0.2)$

---

## 3. LOGIK-BLOCK A: EXIT-RADAR (Nur für 'LONG')
Berechne das spezifische Risiko ($S_{micro}$ von 0-10):
- Cycle-Exhaustion: Pi-Cycle Cross aktiv (+5 Punkte).
- GEX-Wall (Type B): Preis an Call-Wand + fallendes Gamma (+3 Punkte).
- BTC-Lag (Type A): Aktie fällt deutlich stärker als BTC (+2 Punkte).
- OBV-Distribution (Type A): Preis macht Higher High, OBV macht Lower High (+2 Punkte).

---

## 4. LOGIK-BLOCK B: ENTRY-HUNTER (Nur für 'CASH')
Prüfe Kaufsignale (Nur aktiv, wenn $S_{macro} < 7.0$ UND btc_status == LONG):
1. GEX-Flip (Type B): Wechsel von negativem zu positivem Gamma (Zwingend für BUY).
2. OBV-Divergence (Type A): Bullish Divergence (Zwingend für BUY).
3. Institutional Flow: Sichtbare Kauf-Prints in Dark Pools.
4. Trend-Reclaim: Preis schließt über dem 20-Tage-SMA.

---

## 5. FINAL CALCULATION
$S_{final} = (S_{macro\_[Typ]} \cdot 0.6) + (S_{micro} \cdot 0.4)$

Action Labels & Mapping:
- 1.0 - 4.5: "BULLISH / SCALE_IN" (Nur verfügbar für CASH-Status).
- 4.6 - 6.5: "NEUTRAL_WATCH" (Halten oder Beobachten).
- 6.6 - 8.5: "REDUCE_50_PERCENT" (Teilverkäufe).
- 8.6 - 10.0: "HARD_EXIT / CASH" (Vollständige Schließung).

---

## 6. OUTPUT-STRUKTUR
Das Ergebnis wird als JSON-String ausgegeben:

{ "timestamp": "ISO-Zeitstempel", "bitcoin_analysis": { "status": "LONG / CASH", "cycle_phase": "ACCUMULATION / EXPANSION / DISTRIBUTION", "key_metrics": { "mvrv": 0.0, "prod_cost_delta": "+5%" } }, "tickers": [ { "id": "TICKER", "type": "A/B", "final_score": 0.0, "action": "LABEL", "logic_notes": ["Trigger Details"] } ] }

---

### // --- MANUELLE ÄNDERUNGSHINWEISE (V15 -> V16) ---
### // Änderung 1: BTC als binärer Master-Switch eingeführt. Der Bitcoin-Status (LONG/CASH) überschreibt Aktien-Kaufsignale global.
### // Änderung 2: Aggressive Bottom-Logik integriert. MVRV Z-Score Schwelle auf 0.2 angehoben, um die Akkumulation vor dem absoluten Tief zu starten.
### // Änderung 3: Integration der Mining-Produktionskosten (< 110%) als zusätzliche Bestätigung für den Preis-Boden.
### // Änderung 4: Aggressive Top-Logik durch "Pi-Cycle Proximity" (98%). Verkäufe werden initiiert, bevor der Cross physisch stattfindet.
### // Änderung 5: Die Output-Struktur wurde getrennt, um eine isolierte Bewertung des Krypto-Zyklus neben den Aktien-Tickern zu ermöglichen.
### // --- ENDE DER DOKUMENTATION ---