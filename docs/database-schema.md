# Vinvalvet Database Schema

## Syfte

Detta dokument beskriver datamodellen för Vinvalvets egen vin- och produktdatabas.

Målet är att Vinvalvet ska använda en egen kontrollerad datakälla för:

- sökning
- OCR-matchning
- QR-flöden
- framtida AI-matchning
- minskat beroende av externa tjänster

## Arkitektur

Datakälla

↓

Import

↓

JSON / ZIP

↓

Vinvalvet App

↓

Isar

Vinindexet distribueras som versionshanterade JSON- eller ZIP-filer och lagras lokalt i Isar på användarens enhet.

Sökning, OCR-matchning och QR-matchning ska i första hand ske lokalt för hög prestanda, låg driftkostnad och stöd för offline-användning.

## Datamodell: wines

Varje dokument i `wines` representerar ett vin eller en produktpost i Vinvalvets centrala vinindex.

---

## Obligatoriska fält

| Fält | Typ | Beskrivning |
|---|---|---|
| id | string | Internt unikt ID i Vinvalvet |
| productId | string | Produkt-ID från ursprunglig datakälla om tillgängligt |
| name | string | Vinets namn |
| wineType | string | Typ av vin, exempelvis red, white, sparkling eller rose |
| searchTokens | array<string> | Sökbara ord för namn, producent, land, region och alias |
| updatedAt | timestamp | Senaste uppdatering av posten |

---

## Rekommenderade fält

| Fält | Typ | Beskrivning |
|---|---|---|
| producer | string | Producent |
| country | string | Land |
| region | string | Region |
| vintage | number/null | Årgång om känd |
| grapes | array<string> | Druvor |
| aliases | array<string> | Alternativa namn och vanliga sökningar |
| source | string | Ursprungsdatakälla |
| sourceUrl | string/null | Länk till källa om tillgänglig |

---

## Valfria fält

| Fält | Typ | Beskrivning |
|---|---|---|
| qrUrls | array<string> | QR-länkar som kan kopplas till vinet |
| imageUrl | string/null | Bild på flaska eller etikett |
| labelImageUrl | string/null | Bild av etiketten |
| ocrKeywords | array<string> | Nyckelord som hjälper OCR-matchning |
| alcoholPercentage | number/null | Alkoholhalt i procent |
| sugar | number/null | Sockerhalt i gram per liter (g/l) |
| volumeMl | number/null | Volym i milliliter |
| priceSek | number/null | Pris i svenska kronor |
| systembolagetUrl | string/null | Länk till Systembolaget om sådan finns |

---

## Framtida AI-fält

| Fält | Typ | Beskrivning |
|---|---|---|
| embedding | array<number>/null | Vektor för framtida AI-matchning |
| aiDescription | string/null | AI-genererad sammanfattning |
| labelRecognitionHints | array<string> | Hjälpord för bildigenkänning |

---

## Exempelobjekt

```json
{
  "id": "vinvalvet_000001",
  "productId": "12345",
  "name": "Naltros Cava Brut",
  "producer": "Naltros",
  "country": "Spain",
  "region": "Cava",
  "wineType": "sparkling",
  "vintage": null,
  "grapes": ["Macabeo", "Xarel-lo", "Parellada"],
  "aliases": ["Naltros Cava", "Naltros Brut"],
  "searchTokens": [
    "naltros",
    "cava",
    "brut",
    "spain",
    "sparkling"
  ],
  "qrUrls": [],
  "source": "vinvalvet",
  "sourceUrl": null,
  "updatedAt": "2026-06-16T00:00:00Z"
}
```

## Regler

- `name`, `wineType`, `searchTokens` och `updatedAt` ska alltid finnas.
- `grapes`, `aliases`, `qrUrls` och `ocrKeywords` ska vara tomma listor om information saknas.
- Okända textfält bör vara `null` eller tom sträng beroende på framtida importstrategi.
- Årgång ska lagras som `number` när den är känd, annars `null`.
- Sökning i appen ska i första hand baseras på `searchTokens`.
- Vinindexet ska distribueras centralt men användas lokalt via Isar.
- Firestore ska inte användas som primär sökmotor för vinindexet.
