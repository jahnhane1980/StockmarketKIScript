# MISSION: Financial Macro-Handshake (V13 - State Machine)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten (03.04.2026). 
TRENNE Entry- und Exit-Logik vollständig. Kein "Misch-Ergebnis".

---

## 1. PHASE 1: CLASSIFICATION & REGIME-SELECTION
Identifiziere pro Ticker:
1. **TYPE:** (A: Growth/High-Beta | B: Mega-Cap/Index-Leader)
2. **REGIME:** (UP-TREND: Preis > SMA 200 | DOWN-TREND: Preis < SMA 200)
3. **STATUS (Extern):** (LONG oder CASH)

---

## 2. PHASE 2: GLOBAL MACRO (The Environment)
- **Macro-Status:** (Net-Liq, BTC-Proxy, Market Breadth).
- **Macro-Constraint:** Wenn Macro-Score > 7, ist JEDER Entry-Versuch (Block B) blockiert.

---

## 3. LOGIK-BLOCK A: EXIT-RADAR (Nur für 'LONG' Positionen)
Addiere Risiko-Punkte (0-10):
- **SMA-Stretch:** Preis > 35% über 200-SMA (+3)
- **GEX-Wall (Type B):** Preis am oberen Call-Peak + sinkendes GEX (+3)
- **BTC-Lag (Type A):** Aktie fällt, während BTC stagniert (+2)
- **Dark Pool Sells:** Massive Block-Verkäufe auf Tageshoch (+2)
**ACTION:** Score > 8 = **HARD_EXIT** | Score 6-7 = **REDUCE_50%**

---

## 4. LOGIK-BLOCK B: ENTRY-HUNTER (Nur für 'CASH' Positionen)
Sammle "Grüne Lichter" (Requirement: Macro-Score < 7):
- **GEX-Flip (Type B):** GEX wechselt von Negativ zu Positiv (Pflicht für Entry)
- **OBV-Divergence (Type A):** Bullish Divergence (Preis LL, OBV HL) (Pflicht für Entry)
- **Institutional Buy-Prints:** Große Kauf-Blöcke in Dark Pools sichtbar.
- **Trend-Reclaim:** Preis schließt über 20-Tage-SMA.
**ACTION:** Alle Pflicht-Signale erfüllt = **RE-ENTRY / SCALE_IN**

---

## 5. OUTPUT-STRUKTUR (JSON)
{
  "timestamp": "ISO",
  "global_macro": { "score": 0-10, "state": "STRICKT/LOOSE" },
  "tickers": [
    {
      "id": "TICKER",
      "current_status": "LONG/CASH",
      "regime": "UP/DOWN-Trend",
      "exit_logic": {
        "active": "true/false",
        "risk_score": 0-10,
        "warnings": ["Liste der Trigger"],
        "action": "HOLD/REDUCE/EXIT"
      },
      "entry_logic": {
        "active": "true/false",
        "ready_to_buy": "true/false",
        "requirements_met": ["Liste"],
        "missing_signals": ["Liste"],
        "action": "WAIT/WATCH/BUY"
      }
    }
  ]
}