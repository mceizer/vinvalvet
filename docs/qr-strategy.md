# Vinvalvet QR Strategy

## Syfte

Detta dokument beskriver hur QR-koder ska användas för att identifiera produkter i Vinvalvet.

QR ska på sikt ersätta EAN som primär metod för automatisk identifiering av vinflaskor.

Målet är att ge snabbare, mer träffsäkra och mer framtidssäkra produktmatchningar.

---

## Grundflöde

```text
QR-kod
    ↓
URL
    ↓
Producent-ID
    ↓
Vinvalvet-databas
    ↓
Produkt
```

När en QR-kod skannas ska Vinvalvet analysera innehållet och försöka koppla det till en produkt i vinindexet.

---

## Prioriterad strategi

### 1. Direkt produktmatchning

Om QR-koden innehåller ett produkt-ID eller annan unik identifierare:

```text
QR
    ↓
Produkt-ID
    ↓
Direkt träff
```

Produkten kan då identifieras utan ytterligare sökning.

---

### 2. Producentmatchning

Om QR-koden leder till en producentwebbplats:

```text
QR
    ↓
Producent
    ↓
Producent-ID
    ↓
Vinvalvet-databas
```

Vinvalvet försöker identifiera aktuell produkt genom information från producenten.

---

### 3. URL-analys

Om QR-koden innehåller en URL:

```text
QR
    ↓
URL
    ↓
Domän
    ↓
Produktinformation
```

Appen analyserar:

- domännamn
- URL-struktur
- produktnamn
- produktnummer
- metadata

---

## Matchningsstrategi

### Direkt träff

Produkten identifieras med hög säkerhet.

Resultatet visas direkt för användaren.

---

### Delvis träff

Systemet hittar flera möjliga kandidater.

Användaren får välja mellan föreslagna produkter.

---

### Ingen träff

Om ingen produkt kan identifieras:

1. OCR kan användas som kompletterande metod.
2. Manuell sökning erbjuds.
3. Informationen kan sparas för framtida förbättring av databasen.

---

## Datakällor

QR-matchning kan använda:

- Vinvalvets vinindex
- Producentdata
- Manuella korrigeringar
- Framtida externa datakällor

---

## Lagring i vinindexet

Följande fält kan användas för QR-relaterad information:

| Fält | Typ | Syfte |
|---|---|---|
| qrUrls | array<string> | Kända QR-relaterade URL:er |
| aliases | array<string> | Alternativa produktnamn |
| sourceUrl | string | Ursprungslänk till producent eller datakälla |

---

## Framtida förbättringar

Möjliga framtida funktioner:

- automatisk identifiering via producenternas QR-system
- AI-baserad URL-analys
- automatisk produktmatchning från webbsidor
- automatisk inläsning av tekniska datablad
- automatisk hämtning av produktbilder

---

## Långsiktigt mål

QR ska vara Vinvalvets primära metod för produktidentifiering.

Systemet ska kunna identifiera produkter med hög träffsäkerhet utan beroende av EAN-koder och samtidigt fungera tillsammans med OCR som reservmetod när QR-informationen är otillräcklig.
