# MISSION: Financial Macro-Handshake (V9 - Auto-Classification & Precision)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten für den heutigen Tag (03.04.2026).
Führe für die Ticker-Liste (NVDA, PLTR, NVTS, TTD, CRM) zuerst eine Klassifizierung durch und wende dann die spezifische Logik an.

---

## 1. PHASE 1: AUTO-CLASSIFICATION (IDENTIFIZIERUNG)
Bevor du die Analyse startest, ordne jeden Ticker anhand dieser Parameter einem Typ zu:

- **TYPE B (Mega-Cap / Index-Driver):** - Marktkapitalisierung > $250 Mrd. **ODER** Top 10 Gewichtung im NDX/SPX.
  - Fokus-Anker: **Nasdaq-GEX & Dark Pool Flow.**
- **TYPE A (Growth / High-Beta / Liquidity-Proxy):** - Marktkapitalisierung < $250 Mrd. **ODER** Beta > 1.3.
  - Fokus-Anker: **Net-Liquidity & BTC-Divergenz.**

---

## 2. PHASE 2: MACRO-SCORING (Basis 60%)
- **Net-Liquidity (Fed BS - TGA - RRP):** >$6T = 1-3 | <$5.5T = 8-10.
- **BTC (Liquiditäts-Proxy):** Uptrend/Stärke = 1-3 | Schwäche/Divergenz = 7-10.
- **Marktbreite (% > SMA 200):** > 70% = 1-3 | < 40% = 8-10.

---

## 3. PHASE 3: TICKER-SPECIFIC MICRO-LOGIC (Basis 40%)

### WENN TYPE A (Liquidity-Focus):
- **BTC-Correlation:** Fällt die Aktie stärker als BTC bei Abwärtstagen? (+1 auf Score)
- **OBV-Check:** Macht der Preis ein HH, aber das Volumen ein LH? (+2 auf Score)
- **SMA-Stretch:** Preis > 35% über 200-Tage-Linie? (+1 auf Score)

### WENN TYPE B (Gamma-Focus):
- **GEX-Wall:** Notiert der Preis am oberen Call-Limit (Positive Gamma Peak)? (+2 auf Score)
- **Dark Pool Prints:** Ungewöhnlich hohe "Sell-Prints" (Block Trades) bei Hochs? (+2 auf Score)
- **Volatility-Check:** Steigt die IV (Implied Volatility), während der Kurs seitwärts läuft? (+1 auf Score)

---

## 4. FINAL CALCULATION (Alert-Score 1-10)
Berechne: $S_{final} = (S_{macro} \cdot 0.6) + (S_{micro} \cdot 0.4)$

- 1-3 -> **"ALL_SYSTEMS_GO"**
- 4-6 -> **"WATCH_DIVERGENCE"**
- 7-8 -> **"REDUCE_50_PERCENT"**
- 9   -> **"HARD_EXIT"**
- 10  -> **"EMERGENCY_CASH"**

---

## 5. OUTPUT-STRUKTUR (JSON)
Liefere AUSSCHLIESSLICH dieses JSON.

{
  "timestamp": "2026-04-03T[TIME]Z",
  "global_alert_avg": [DURCHSCHNITTSSCORE],
  "market_context": {
    "net_liq": "[WERT]",
    "btc_status": "[STATUS]",
    "breadth": "[%]"
  },
  "tickers": [
    {
      "id": "[TICKER]",
      "classification": {
        "type": "[A/B]",
        "reason": "[Market Cap / Beta Begründung]"
      },
      "scores": { "macro": [1-10], "micro": [1-10], "final": [1-10] },
      "action_label": "[STRING]",
      "current_price": "[WERT]",
      "micro_signals": {
        "signal_1": "[Divergenz/GEX Status]",
        "signal_2": "[Institutioneller Flow/BTC Corr]",
        "overstretch": "[SMA-Distanz]"
      },
      "short_info": "[ACTION_LABEL]: [Präzise Begründung warum Typ A/B hier gerade ein Risiko/Chance ist]"
    }
  ]
}