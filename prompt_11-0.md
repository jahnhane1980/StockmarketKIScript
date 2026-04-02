# MISSION: Financial Macro-Handshake & Ticker Classification (2026 Edition)

**ROLE:** Senior Quant Strategist. Deine Aufgabe: Erfasse den globalen Liquiditätsstatus (Echtzeit April 2026) und klassifiziere die Ticker-Liste nach ihrem Korrelations-Fingerabdruck.

---

## SCHRITT 1: REAL-TIME SEARCH (DATA GATHERING)
Suche nach den aktuellsten Werten (Echtzeit) für:
1. **Net-Liquidity:** Trend der letzten 4 Wochen.
2. **Bitcoin (BTC):** Aktueller Preis & Momentum (Liquiditäts-Proxy).
3. **Nasdaq-100 GEX:** Positiv oder Negativ?
4. **Marktbreite:** % der Nasdaq-Aktien über SMA 200.

---

## SCHRITT 2: MACRO SCORING (1-10)
Bewerte das Risiko (1=Bullisch, 10=Bärisch) für:
- Net-Liquidity / BTC-Momentum / GEX-Mechanik / Marktbreite.

---

## SCHRITT 3: TICKER-CLASSIFICATION & INFO
Analysiere die Liste. Ordne jeden Ticker zu (**Typ A: Liquiditäts-Junkie** oder **Typ B: Index-Soldat**). 
**Zusätzlich:** Erstelle für jeden Ticker eine kurze "Action-Info" (2-3 Sätze): 
- Warum dieser Typ? 
- Was ist die aktuelle "Gefahr" oder "Chance" bei diesem spezifischen Wert?

---

## SCHRITT 4: OUTPUT (JSON & MARKDOWN)
1. Markdown-Zusammenfassung inkl. Ticker-Infos.
2. Valides JSON-Objekt für Expo-Dashboard-Integration.

**TICKER-LISTE:** [DEINE TICKER HIER]


{
  "timestamp": "2025-10-10T10:00:00Z",
  "global_alert": 6.8, 
  "global_idicators": {
  	"Net-Liquidity": {
  		"interpretation" : "Stagnierend ($5.92T)",
  		"value-scale": "6 / 10",
  		"signal" : "Neutral/Negativ"
  		},
  	"BTC" : {
  		"interpretation" : "~122.000 $ (Lower High)",
  		"value-scale": "8 / 10",
  		"signal" : "Divergenz-Warnung"  		
  		},
  	"Nasdaq-GEX": {
  		"interpretation" : "+ 0.5B (Sinkend)",
  		"value-scale": "5 / 10",
  		"signal" : "Abnehmender Schutz"  		
  		},
  	"Nasdaq-Marktbreite": {
  		"interpretation" : "41% > SMA 200",
  		"value-scale": "8 / 10",
  		"signal" : "Extreme Schwäche"  		
  	}
  },
  "tickers": [
    {
      "id": "NVTS",
      "type": "A",
      "anchor": "BTC_LIQUIDITY",
      "alert_score": 9,
      "ath" :"17,79",
      "currency": "$",
      "current_price":"15,69",
      "short_info": "Extremes Risiko. Bitcoin-Divergenz signalisiert Liquiditäts-Exit. Small-Cap Schwäche ignoriert Nasdaq-Hochs."
    },
    {
      "id": "NVDA",
      "type": "B",
      "anchor": "NDX_GEX",
      "alert_score": 4,
      "ath" :"178,40",
      "currency": "$",
      "current_price":"167,40",      
      "short_info": "Index-Leader. Profitiert von Kapital-Rotation aus Small-Caps. Mechanisch gestützt durch positives Gamma."
    }
  ]
}

https://www.alphavantage.co/query?function=SYMBOL_SEARCH&keywords=TESLA&apikey=DEMO

  "BTC-Analyse": {
  	"???" : "???"
  },
  "Gold-Analyse": {
  	"...": ""
  },