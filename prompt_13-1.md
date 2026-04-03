# MISSION: Financial Macro-Handshake (V7 - Verified Action-Mapping)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten für den [DATUM]. Ignoriere deine Wissensdatenbank. Halluzinationen führen zum System-Ausfall.

---
## 1. ANALYSE-LOGIK (Scoring-Regeln 1-10 für `alert_score` )
- **Net-Liquidity (Fed BS - TGA - RRP):** >$6T = 1-3 | <$5.5T = 8-10.
- **BTC (Liquiditäts-Proxy):** Uptrend = 1-3 | Downtrend/Divergenz = 7-10.
- **Nasdaq-GEX:** > +$2B = 1-3 | < 0 (Negativ) = 9-10.
- **Marktbreite (% > SMA 200):** > 70% = 1-3 | < 40% = 8-10.

## 1. ACTION-MAPPING LOGIK (Zahlen-String-Paare)
Ordne den `alert_score` (1-10) zwingend einem dieser `action_label` zu:
- 1-3 -> "ALL_SYSTEMS_GO"
- 4-6 -> "WATCH_DIVERGENCE"
- 7-8 -> "REDUCE_50_PERCENT"
- 9   -> "HARD_EXIT"
- 10  -> "EMERGENCY_CASH"

## 3. ANCHOR-DEFINITIONEN
- **TYPE A (Anchor: `BTC_LIQUIDITY`):** High Beta / Small-Caps. Sensor: Bitcoin.
- **TYPE B (Anchor: `NDX_GEX`):** Mega-Caps. Sensor: Nasdaq Gamma Exposure.

---

## 4. OUTPUT-STRUKTUR (STRIKTE JSON-VORGABE)
Liefere AUSSCHLIESSLICH dieses JSON. Jedes Datenfeld benötigt URL und Timestamp.

{
  "timestamp": "2026-04-02T15:05:00Z",
  "global_alert": [DURCHSCHNITTSSCORE],
  "global_indicators": {
    "Net-Liquidity": { "val": "[Zahl]", "score": "[1-10]", "source": "[URL]", "last_updated": "[ISO]" },
    "BTC": { "val": "[Preis]", "score": "[1-10]", "source": "[URL]", "last_updated": "[ISO]" },
    "Nasdaq-GEX": { "val": "[Zahl]", "score": "[1-10]", "source": "[URL]", "last_updated": "[ISO]" }
  },
  "tickers": [
    {
      "id": "[TICKER]",
      "type": "[A oder B]",
      "anchor": "[BTC_LIQUIDITY oder NDX_GEX]",
      "alert_score": [1-10],
      "action_label": "[STRING AUS PUNKT 1]",
      "current_price": "[WERT]",
      "source": "[URL]",
      "logic_check": "[Begründung Anchor & Score]",
      "short_info": "[ACTION_LABEL]: [Kurzer Analyse-Satz]"
    }
  ]
}

**TICKER-LISTE:** NVDA, PLTR, NVTS, TTD, CRM