# MISSION: Financial Macro-Handshake (JSON-Schema V2 - VERIFIED DATA)

**STOP-BEFEHL:** Du darfst NICHT aus dem Gedächtnis antworten. Nutze zwingend dein Such-Tool, um Echtzeit-Daten für den heutigen Tag (April 2026) zu finden. Halluzinationen bei Aktienkursen sind strikt untersagt.

---

## 1. ANALYSE-LOGIK (Scoring-Regeln 1-10)
- **Net-Liquidity (Fed BS - TGA - RRP):** >$6T = 1-3 | <$5.5T = 8-10.
- **BTC (Liquiditäts-Proxy):** Uptrend = 1-3 | Downtrend/Divergenz = 7-10.
- **Nasdaq-GEX:** > +$2B = 1-3 | < 0 (Negativ) = 9-10.
- **Marktbreite (% > SMA 200):** > 70% = 1-3 | < 40% = 8-10.

---

## 2. OUTPUT-STRUKTUR (STRIKTE JSON-VORGABE)
Jedes Item MUSS eine Quelle (URL) und einen Zeitstempel enthalten.

{
  "timestamp": "[ISO-ZEITSTEMPEL]",
  "global_alert": [DURCHSCHNITTSSCORE 1-10], 
  "global_idicators": {
    "Net-Liquidity": { 
      "interpretation": "[Text]", 
      "value_scale": "[Score]/10", 
      "source": "[URL]", 
      "last_updated": "[ZEIT]" 
    },
    "BTC": { 
      "interpretation": "[Text]", 
      "value_scale": "[Score]/10", 
      "source": "[URL]", 
      "last_updated": "[ZEIT]" 
    },
    "Nasdaq-GEX": { 
      "interpretation": "[Text]", 
      "value_scale": "[Score]/10", 
      "source": "[URL]", 
      "last_updated": "[ZEIT]" 
    },
    "Nasdaq-Marktbreite": { 
      "interpretation": "[Text]", 
      "value_scale": "[Score]/10", 
      "source": "[URL]", 
      "last_updated": "[ZEIT]" 
    }
  },
  "tickers": [
    {
      "id": "[TICKER]",
      "type": "[A/B]",
      "anchor": "[BTC_LIQUIDITY oder NDX_GEX]",
      "alert_score": [1-10],
      "ath_52w": "[WERT]",
      "current_price": "[WERT]",
      "currency": "$",
      "source": "[URL]",
      "last_updated": "[ZEIT]",
      "short_info": "[MAX 2 SÄTZE]"
    }
  ]
}

**TICKER-LISTE:** NVDA, PLTR, NVTS, TTD, CRM

p