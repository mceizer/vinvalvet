# Vinvalvet Data Sources

## Syfte

Detta dokument beskriver vilka datakällor som används eller planeras för Vinvalvets vinindex.

Målet är att Vinvalvet på sikt ska bygga upp en egen och oberoende databas med hög datakvalitet, snabb sökning och minimalt beroende av externa tjänster.

---

## Aktiva datakällor

### C4illin

**Status:** Aktiv

**Syfte:**

Nuvarande primära källa för produkt- och vininformation.

**Användningsområden:**

- sökning
- OCR-matchning
- produktidentifiering
- produktmetadata

**Kommentar:**

C4illin används som grundkälla under uppbyggnaden av Vinvalvets egen databas.

---

## Planerade datakällor

### Systembolaget

**Status:** Planerad

**Syfte:**

Officiell produktinformation för produkter som säljs via Systembolaget.

**Möjliga användningsområden:**

- produktnamn
- producent
- region
- land
- alkoholhalt
- sockerhalt
- volym
- pris

---

### Producenter

**Status:** Planerad

**Syfte:**

Kompletterande information direkt från vinproducenter.

**Möjliga användningsområden:**

- druvsammansättning
- produktbeskrivningar
- produktbilder
- QR-relaterad information
- tekniska datablad

---

### Egna importer

**Status:** Planerad

**Syfte:**

Importer skapade och kontrollerade av Vinvalvet.

**Möjliga användningsområden:**

- historiska data
- specialsortiment
- kompletteringar som saknas i externa källor
- datakorrigeringar

---

### Manuella korrigeringar

**Status:** Planerad

**Syfte:**

Korrigeringar och förbättringar som görs manuellt av Vinvalvet.

**Möjliga användningsområden:**

- rättning av felaktiga produkter
- förbättrade söktermer
- alias och alternativa namn
- OCR-förbättringar
- QR-förbättringar

---

## Prioritetsordning

När flera datakällor innehåller samma information ska följande prioritet användas:

1. Manuella korrigeringar
2. Egna importer
3. Producentdata
4. Systembolagsdata
5. C4illin

---

## Långsiktigt mål

Målet är att Vinvalvet ska kunna underhålla ett eget vinindex med minimal beroendeställning till externa tjänster.

C4illin används initialt som grundkälla men ska på sikt kunna ersättas av Vinvalvets egna datakällor och importflöden.
