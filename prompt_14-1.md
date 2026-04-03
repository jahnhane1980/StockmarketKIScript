# MISSION: Financial Macro-Handshake (V10 - FULL CYCLE)

**STRIKTE ANWEISUNG:** Suche per Websuche nach Echtzeit-Daten für heute (03.04.2026). 
Dieses Skript identifiziert nun sowohl **EXIT-GEFAHREN** als auch **ENTRY-CHANCEN**.

---

## 1. PHASE 1: AUTO-CLASSIFICATION (IDENTIFIZIERUNG)
- **TYPE B (Mega-Cap):** Cap > $250 Mrd. | Fokus: **GEX, Dark Pool, Gamma-Flip.**
- **TYPE A (Growth):** Cap < $250 Mrd. | Fokus: **Net-Liq, BTC-Corr, OBV-Divergenz.**

---

## 2. PHASE 2: GLOBAL RECOVERY & RISK (Basis 60%)
- **Net-Liquidity:** >$6T = Score 1-2 | <$5.5T = Score 9-10.
- **Breadth Thrust:** Anteil > 200 SMA steigt von <40% rapide an = **-2 auf Score** (Kaufsignal).
- **BTC Lead:** BTC steigt, während NDX stagniert = **-1 auf Score** (Risk-On Vorlauf).

---

## 3. PHASE 3: TICKER-SPECIFIC MICRO-LOGIC (Basis 40%)

### WENN TYPE A (Entry/Exit Signale):
- **BULLISH DIVERGENCE:** Preis LL, OBV HL (Akkumulation) = **-3 auf Score**.
- **BEARISH DIVERGENCE:** Preis HH, OBV LH (Distribution) = **+2 auf Score**.
- **BTC RECOVERY:** Aktie bricht über 20-Tage-Linie, während BTC steigt = **-2 auf Score**.

### WENN TYPE B (Entry/Exit Signale):
- **GAMMA-FLIP:** GEX springt von negativ auf positiv = **-3 auf Score** (Kaufzwang MM).
- **DARK POOL BUY-PRINTS:** Massive Kauf-Blöcke am Boden sichtbar = **-2 auf Score**.
- **IV-CRUSH:** Vola sinkt bei steigenden Kursen = **-1 auf Score**.

---

## 4. FINAL ACTION-MAPPING (1-10)
Berechne: $S_{final} = (S_{macro} \cdot 0.6) + (S_{micro} \cdot 0.4)$

- **1-2  -> "ALL_IN / AGGRESSIVE_BUY"** (Makro & Micro sind grün)
- **3-4  -> "SCALE_IN / BULLISH"** (Erste Positionen aufbauen)
- **5-6  -> "NEUTRAL_WATCH"** (Keine klare Richtung)
- **7-8  -> "REDUCE_50_PERCENT"** (Gewinne sichern / Teil-Exit)
- **9-10 -> "HARD_EXIT / CASH_ONLY"** (Vollständiger Schutz)

---

## 5. OUTPUT-STRUKTUR (JSON)
Liefere AUSSCHLIESSLICH dieses JSON.

{
  "timestamp": "2026-04-03T[TIME]Z",
  "cycle_phase": "[ACCUMULATION / DISTRIBUTION / PANIC]",
  "tickers": [
    {
      "id": "[TICKER]",
      "type": "[A/B]",
      "final_score": [1-10],
      "action_label": "[STRING]",
      "entry_logic": "[Was müsste passieren, damit der Score sinkt?]",
      "exit_logic": "[Was triggert den Hard Exit?]",
      "signals": {
        "macro_tide": "[Richtung der Liquidität]",
        "micro_flow": "[OBV oder GEX Status]",
        "institutional": "[Dark Pool / BTC Status]"
      },
      "short_info": "[ACTION_LABEL]: [Satz zum aktuellen Stand im Zyklus]"
    }
  ]
}