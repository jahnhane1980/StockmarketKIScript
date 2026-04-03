# MISSION: Financial Macro-Handshake (V12 - Full-Cycle Agent & Production Structure)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten für den 03.04.2026. 
Keine Kürzung der Output-Struktur. Absolute Einhaltung der mathematischen Gewichtung.

---

## 1. PHASE 1: AUTO-CLASSIFICATION (IDENTIFIZIERUNG)
- **TYPE B (Mega-Cap / Index-Driver):** Cap > $250 Mrd. **ODER** Top 10 Gewichtung im NDX/SPX.
  - Fokus: **GEX, Dark Pool Flow, IV-Crush.**
- **TYPE A (Growth / High-Beta):** Cap < $250 Mrd. **ODER** Beta > 1.3.
  - Fokus: **Net-Liquidity, BTC-Divergenz, OBV.**

---

## 2. PHASE 2: GLOBAL MACRO-SCORING (Gewichtung 60%)
- **Net-Liquidity (Fed BS - TGA - RRP):** >$6T = 1-3 | <$5.5T = 8-10.
- **BTC (Liquiditäts-Proxy):** Trend-Bestätigung = 1-3 | Divergenz/Bruch = 7-10.
- **Marktbreite (% > SMA 200):** > 70% = 1-3 | < 40% = 8-10.

---

## 3. PHASE 3: TICKER-SPECIFIC MICRO-LOGIC (Gewichtung 40%)

### WENN TYPE A (Entry/Exit Signale):
- **BULLISH DIVERGENCE (Preis LL, OBV HL):** -3 auf Micro-Score.
- **BEARISH DIVERGENCE (Preis HH, OBV LH):** +3 auf Micro-Score.
- **BTC RECOVERY:** Aktie bricht über 20-Tage-SMA bei BTC-Stärke = -2 auf Score.

### WENN TYPE B (Entry/Exit Signale):
- **GAMMA-FLIP:** GEX springt von negativ auf positiv = -3 auf Score.
- **DARK POOL SELL-PRINTS:** Massive Block-Verkäufe bei Hochs = +2 auf Score.
- **IV-CRUSH:** Vola sinkt bei steigenden Kursen = -1 auf Score.

---

## 4. PHASE 4: FINAL CALCULATION & LOGIC-GUARD
**Formel:** $S_{final} = (S_{macro} \cdot 0.6) + (S_{micro} \cdot 0.4)$

**LOGIC-GUARD:** Wenn $S_{macro} > 7$, darf $S_{final}$ nicht kleiner als **5.0** sein.

---

## 5. ACTION-MAPPING
- **1.0 - 2.5  -> "AGGRESSIVE_BUY"**
- **2.6 - 4.5  -> "SCALE_IN / BULLISH"**
- **4.6 - 6.5  -> "NEUTRAL_WATCH"**
- **6.6 - 8.5  -> "REDUCE_50_PERCENT"**
- **8.6 - 10.0 -> "HARD_EXIT / CASH"**

---

## 6. OUTPUT-STRUKTUR (STRIKTE JSON-VORGABE)
Liefere das JSON mit allen unten genannten Feldern.

{
  "timestamp": "[ISO]",
  "global_alert_avg": [0-10],
  "market_context": {
    "net_liq": "[WERT]",
    "btc_status": "[STATUS]",
    "breadth": "[%]"
  },
  "cycle_phase": "[ACCUMULATION/DISTRIBUTION/PANIC]",
  "logic_guard_active": [true/false],
  "tickers": [
    {
      "id": "[TICKER]",
      "classification": { "type": "[A/B]", "reason": "[BEGRÜNDUNG]" },
      "scores": { "macro": [0-10], "micro": [0-10], "final": [0-10] },
      "action_label": "[STRING]",
      "current_price": "[WERT]",
      "micro_signals": {
        "signal_1": "[Divergenz/GEX]",
        "signal_2": "[Flow/BTC]",
        "overstretch": "[SMA-Distanz]"
      },
      "entry_logic": "[BEDINGUNG]",
      "exit_logic": "[BEDINGUNG]",
      "short_info": "[TEXT]"
    }
  ]
}