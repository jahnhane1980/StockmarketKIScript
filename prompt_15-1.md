# MISSION: Financial Macro-Handshake (V14 - Full-Regime API Edition)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten für den 03.04.2026. 
Keine Halluzinationen. Keine Kürzung der Output-Struktur. Absolute Einhaltung der mathematischen Gewichtung und des Logic-Guards.

---

## 0. INPUT INTERFACE (Eingabe-Spezifikation)
Das Skript erwartet die Eingangsdaten für die automatisierte Verarbeitung in folgendem Format:

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

## 1. PHASE 1: AUTO-CLASSIFICATION & REGIME-SELECTION
Identifiziere jeden Ticker automatisch anhand von Marktdaten:
- **TYPE B (Mega-Cap / Index-Driver):** Cap > $250 Mrd. (Fokus: GEX, Dark Pool Flow, Institutional Prints).
- **TYPE A (Growth / High-Beta):** Cap < $250 Mrd. (Fokus: Net-Liquidity, BTC-Proxy, OBV-Divergenz).

Regime-Auswahl basierend auf dem bereitgestellten `status`:
- `status: LONG` -> Aktiviere **LOGIK-BLOCK A (EXIT-RADAR)**.
- `status: CASH` -> Aktiviere **LOGIK-BLOCK B (ENTRY-HUNTER)**.

---

## 2. PHASE 2: GLOBAL MACRO-SCORING (Gewichtung 60%)
Berechne den globalen Makro-Status ($S_{macro}$):
- **Net-Liquidity (Fed BS - TGA - RRP):** >$6T = 1-3 | <$5.5T = 8-10.
- **BTC (Liquiditäts-Proxy):** Trend-Bestätigung = 1-3 | Divergenz/Bruch = 7-10.
- **Marktbreite (% > SMA 200):** > 70% = 1-3 | < 40% = 8-10.

**LOGIC-GUARD:** Wenn $S_{macro} > 7.0$, wird das Feld `ready_to_buy` für alle `CASH`-Ticker zwingend auf `false` gesetzt. Ein Einstieg ist bei diesem Marktrisiko untersagt.

---

## 3. LOGIK-BLOCK A: EXIT-RADAR (Nur für 'LONG' Status)
Berechne das spezifische Risiko ($S_{micro}$ von 0-10):
- **SMA-Stretch:** Preis > 35% über 200-Tage-Linie (+3 Punkte).
- **GEX-Wall (Type B):** Preis an Call-Wand + fallendes Gamma (+3 Punkte).
- **Dark Pool Sells (Type B):** Massive institutionelle Verkaufs-Blöcke (+2 Punkte).
- **BTC-Lag (Type A):** Aktie fällt deutlich stärker als BTC (+2 Punkte).
- **OBV-Distribution (Type A):** Preis macht Higher High, OBV macht Lower High (+2 Punkte).

---

## 4. LOGIK-BLOCK B: ENTRY-HUNTER (Nur für 'CASH' Status)
Prüfe Kaufsignale (Aktiviert nur, wenn Macro-Logic-Guard = `false`):
- **GEX-Flip (Type B):** Wechsel von negativem zu positivem Gamma (Zwingend für BUY).
- **OBV-Divergence (Type A):** Bullish Divergence (Preis LL, OBV HL) (Zwingend für BUY).
- **Institutional Flow:** Sichtbare Kauf-Prints in Dark Pools (Zusatz-Signal).
- **Trend-Reclaim:** Preis schließt über dem 20-Tage-SMA (Bestätigungssignal).

---

## 5. FINAL CALCULATION
Der finale Score berechnet sich aus:
$$S_{final} = (S_{macro} \cdot 0.6) + (S_{micro} \cdot 0.4)$$

**Action Labels & Mapping:**
- 1.0 - 4.5: **"BULLISH / SCALE_IN"** (Nur verfügbar für `CASH`-Status).
- 4.6 - 6.5: **"NEUTRAL_WATCH"** (Halten oder Beobachten, kein Handlungsbedarf).
- 6.6 - 8.5: **"REDUCE_50_PERCENT"** (Teilverkäufe zur Risikominimierung).
- 8.6 - 10.0: **"HARD_EXIT / CASH"** (Vollständige Schließung der Position).