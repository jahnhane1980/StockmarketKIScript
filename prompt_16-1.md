# MISSION: Financial Macro-Handshake (V16.2 - Yield-Correlation & Volume-Climax)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten (Stichtag: 03.04.2026). Der Bitcoin-Status ist nun dreifach gesichert: Value (MVRV), Momentum (Volume-Climax) und Makro-Liquidity (Yields/NetLiq).

---

## 0. INPUT INTERFACE
Das Skript verarbeitet die Eingangsdaten in diesem Format (JSON-String):

{
  "analysis_request": {
    "macro_metrics": {
      "us10y_yield": 4.31,
      "btc_volume_24h": 47340000000,
      "fed_net_liq": 5782000000000,
      "weekly_rsi": 28.5,
      "mvrv_z": 0.47
    },
    "tickers": [
      { "id": "NVDA", "status": "CASH" },
      { "id": "PLTR", "status": "CASH" }
    ]
  }
}

---

## 1. PHASE 1: BTC MASTER-SWITCH (The "No-Liquidity-No-Trade" Rule)
Der Status LONG wird nur vergeben, wenn die Liquidität und die Panik den "Value" bestätigen.

### A. Bottom-Finder (Kapitulations-Check)
Setze btc_status = LONG nur, wenn BEIDE Bedingungen erfüllt sind:
1. Value & Momentum: (MVRV Z-Score < 0.1 ODER Weekly RSI < 30) UND (Handelsvolumen > 150% des 30-Tage-Schnitts = Climax-Event).
2. Yield-Guard: Die US-10-Jahres-Rendite (US10Y) darf innerhalb der letzten 5 Handelstage nicht um mehr als 5% absolut gestiegen sein (Verhinderung von "Rate-Shock"-Exits).

### B. Liquidity-Veto (Der Stecker-Zieher)
Setze btc_status zwingend auf CASH/VETO, wenn:
- Die Korrelation zwischen BTC und US10Y stark negativ ist (BTC fällt massiv, während Zinsen steigen) UND die Netto-Liquidität (NetLiq = WALCL - TGA) im 4-Wochen-Trend sinkt.
- Logik: Ein "günstiger" Preis wird ignoriert, wenn der Zinsmarkt den Exit erzwingt.

---

## 2. PHASE 2: AUTO-CLASSIFICATION & WEIGHTING
Identifiziere Ticker-Typen automatisch:
- TYPE B (Mega-Cap): Marktkapitalisierung > $250 Mrd. (NVDA, CRM).
- TYPE A (Growth): Marktkapitalisierung < $250 Mrd. (PLTR, NVTS).

### Dynamische Makro-Scores (S_macro)
- Global Yield Penalty: Wenn US10Y > 4.25% und steigend: Addiere pauschal +2.0 auf alle Scores.
- Gewichtung TYPE A: S_macro_A = (S_BTC * 0.6) + (S_Liquidity * 0.4)
- Gewichtung TYPE B: S_macro_B = (S_BTC * 0.3) + (S_Liquidity * 0.5) + (S_Breadth * 0.2)

---

## 3. LOGIK-BLOCK A: EXIT-RADAR (Nur für 'LONG')
Berechne das spezifische Risiko (S_micro von 0-10):
- Yield-Spike: US10Y steigt > 0.15% innerhalb eines Tages (+4 Punkte).
- BTC-Lag (Type A): Aktie fällt deutlich stärker als BTC (+2 Punkte).
- OBV-Distribution: Preis macht Higher High, OBV macht Lower High.

---

## 4. LOGIK-BLOCK B: ENTRY-HUNTER (Nur für 'CASH')
Prüfe Kaufsignale (Nur aktiv, wenn S_macro < 6.0 UND btc_status == LONG):
1. Yield-Stabilization: US10Y flacht ab oder sinkt (Zwingend für Tech-Käufe).
2. Volume-Confirmation: Steigendes Volumen bei positivem Preis-Tag (Bestätigung des Climax).
3. OBV-Divergence: Bullish Divergence bei Typ A Tickers.

---

## 5. FINAL CALCULATION & OUTPUT-STRUKTUR
S_final = (S_macro * 0.6) + (S_micro * 0.4)

Mapping:
- 1.0 - 4.5: "BULLISH / SCALE_IN"
- 4.6 - 6.5: "NEUTRAL_WATCH"
- 6.6 - 10.0: "HARD_EXIT / CASH"

Das Ergebnis wird als JSON-String ausgegeben:

{
  "timestamp": "ISO-Zeitstempel",
  "macro_context": {
    "btc_status": "VETOED / CASH",
    "yield_pressure": "HIGH / LOW",
    "liquidity_trend": "DRAINING / NEUTRAL / EXPANDING"
  },
  "tickers": [
    {
      "id": "TICKER",
      "final_score": 0.0,
      "action": "LABEL",
      "logic_notes": ["Details zu Yields, Volume und Liquidity-Veto"]
    }
  ]
}

---

### // --- MANUELLE ÄNDERUNGSHINWEISE (V16.1 -> V16.2) ---
### // Änderung 1: Vollständige Entfernung von SMA und COP (Produktionskosten). In einem Marktumfeld mit "Broken Liquidity" sind diese Werte zu träge und bieten keinen Schutz vor systemischen Abverkäufen.
### // Änderung 2: Einführung des "Yield-Guards". Da Tech-Titel (Typ A/B) mathematisch an den Zinsen hängen, blockiert ein schneller Zinsanstieg (US10Y) nun alle Kaufsignale, egal wie tief Bitcoin notiert.
### // Änderung 3: Integration des "Volume-Climax". Käufe werden nur noch erlaubt, wenn ein Panik-Volumen (>150% Durchschnitt) stattgefunden hat, um das "Greifen in das fallende Messer" zu verhindern.
### // Änderung 4: Das "Liquidity-Veto" prüft nun die Netto-Liquidität (Fed-Bilanz minus TGA). Sinkt diese, wird der Master-Switch auf CASH gesetzt, da dem System der Treibstoff für eine Erholung fehlt.
### // Änderung 5: Anpassung der Gewichtung für Typ A (Growth). Da diese Titel extrem liquiditätsgetrieben sind, wurde der S_Liquidity Anteil auf 40% erhöht.
### // --- ENDE DER DOKUMENTATION ---