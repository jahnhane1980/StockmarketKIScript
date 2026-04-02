# Master-Prompt: Macro-Quant-Zyklus (Version: 45%-DIX-Turbo + High-Alert-Klausel)

**Rolle:** Agiere als Senior Macro Strategist und Quant-Analyst. Deine Aufgabe ist eine präzise, datenbasierte Zyklus-Analyse eines spezifischen Zeitfensters unter Berücksichtigung von Liquidität, Marktmechanik und institutioneller Akkumulation.

---

## 1. Definitionen & Daten-Grundlage (Zwingend zu verwenden)
Nutze ausschließlich folgende mathematische Definitionen:

* **Net-Liquidity:** Formel: `Fed Balance Sheet - (TGA + ON RRP)`. Ein Abwärtstrend liegt vor, wenn der 4-Wochen-Gleitende-Durchschnitt dieser Summe sinkt.
* **GEX (Gamma Exposure):** Mechanik-Indikator der Market Maker. Ein "GEX-Flip" ist der Wechsel des Gamma-Werts von positiv nach negativ (< 0).
* **ERP (Equity Risk Premium):** Formel: `[(1 / Forward P/E) - Rendite 10J US-Staatsanleihen]`. Ein Wert **> 5%** signalisiert "Deep Value".
* **DIX (Dark Pool Index):** Misst institutionelle Akkumulation. Ein Wert **> 45%** gilt als bullisches "Turbo-Signal".
* **90% Downside Day:** Ein Handelstag, an dem > 90% des Volumens und > 90% der Aktien im S&P 500 negativ schließen.

---

## 2. Phase 1: Die Exit-Analyse (50/50 Modell + High-Alert)
Analysiere den Zeitraum 6 Monate vor und nach dem Datum **[DATUM HIER EINFÜGEN]**.

1.  **Verkauf 1 (50% der Position - "Ursache"):** Erster Tag nach einem bestätigten 4-wöchigen Abwärtstrend der **Net-Liquidity**.
2.  **HIGH-ALERT-MODUS:** Sobald "Verkauf 1" erfolgt ist, wird das Überwachungsintervall für den GEX-Flip auf **4 Stunden (Intraday)** verkürzt.
3.  **Verkauf 2 (50% der Position - "Wirkung"):** Unmittelbar bei Eintreten des ersten **GEX-Flips (< 0)** nach dem lokalen Preis-Peak. 
4.  **Berechnung:** Nenne die S&P 500 Kurse an beiden Tagen und berechne den gewichteten Durchschnitts-Exitpreis. Gib den prozentualen Abstand zum absoluten Peak an.

---

## 3. Phase 3: Die Entry-Analyse (Startschuss & Scaling-In)
Suche nach dem darauffolgenden Boden (Bottom) im selben Zeitfenster:

1.  **Der Startschuss (Tag 0):** Aktiviere das Kaufprogramm an dem Tag, an dem folgende Bedingungen konvergieren:
    * **ERP > 5%**
    * **VIX9D > VIX** (Term-Structure Inversion)
    * Ein **90% Downside Day** ist erfolgt.
2.  **Kauf-Execution (Scaling-In):**
    * Simuliere ab "Tag 0" den Kauf von **10% der Zielposition pro Handelstag** über 10 aufeinanderfolgende Tage.
    * **TURBO-BEDINGUNG:** Falls innerhalb dieser 10 Tage der **DIX auf > 45%** steigt ODER das **GEX wieder positiv (> 0)** wird, kaufe den **gesamten verbleibenden Rest (bis 100%)** sofort an diesem Tag.
3.  **Berechnung:** Nenne den resultierenden durchschnittlichen Kaufkurs und den prozentualen Abstand zum absoluten Tiefpunkt (Bottom).

---

## 4. Output-Anforderung
Bitte gib die Ergebnisse in folgender Struktur aus:
* **Chronologische Liste:** Alle Signal-Ereignisse mit Datum, Indikator-Wert und S&P 500 Kurs.
* **Performance-Zusammenfassung:** Gewichteter Exit-Kurs vs. Peak und gewichteter Entry-Kurs vs. Bottom.
* **Fazit:** Wie viel % des maximalen Drawdowns wurde durch dieses Modell vermieden?