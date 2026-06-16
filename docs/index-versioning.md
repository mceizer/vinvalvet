# Vinvalvet Index Versioning

## Syfte

Detta dokument beskriver hur Vinvalvet hanterar versionering och uppdatering av vinindexet.

Målet är att appen automatiskt ska kunna avgöra om en ny version av vinindexet finns tillgänglig och vid behov ladda ner och importera den lokalt.

---

## Versionshantering

Varje publicerad version av vinindexet ska ha ett unikt versionsnummer.

### Rekommenderat format

```text
YYYY.MM.DD
```

### Exempel

```text
2026.06.16
2026.06.23
2026.07.01
```

Alternativt kan versionsnummer kompletteras med revisionsnummer vid flera publiceringar samma dag.

Exempel:

```text
2026.06.16.1
2026.06.16.2
```

---

## Metadatafil

Varje publicerad version ska ha en metadatafil som beskriver aktuell version.

### Exempel

```json
{
  "version": "2026.06.16",
  "generatedAt": "2026-06-16T20:00:00Z",
  "wineCount": 45231,
  "downloadUrl": "https://..."
}
```

### Fält

| Fält | Typ | Beskrivning |
|---|---|---|
| version | string | Aktuell version av vinindexet |
| generatedAt | datetime | Tidpunkt då indexet genererades |
| wineCount | number | Antal produkter i indexet |
| downloadUrl | string | URL till aktuell JSON- eller ZIP-fil |

---

## Uppdateringsflöde

Vid appstart eller vid manuell kontroll ska följande process användas:

```text
Start
  ↓
Kontrollera version
  ↓
Nyare version?
  ↓
Ja
  ↓
Ladda ner
  ↓
Verifiera fil
  ↓
Importera till Isar
  ↓
Klar
```

Om ingen nyare version finns fortsätter appen att använda det lokala indexet.

---

## Lokal lagring

Den senaste installerade versionen ska lagras lokalt i appen.

Exempel:

```json
{
  "installedVersion": "2026.06.16"
}
```

Appen jämför den lokala versionen med den publicerade versionen innan nedladdning sker.

---

## Felhantering

Om nedladdning eller import misslyckas ska appen:

1. Behålla den tidigare fungerande versionen.
2. Informera användaren om att uppdateringen misslyckades.
3. Tillåta nytt försök vid senare tillfälle.

Ingen uppdatering får ersätta ett fungerande index förrän importen har slutförts utan fel.

---

## Långsiktigt mål

Vinindexet ska kunna uppdateras centralt utan att användaren behöver installera en ny version av Vinvalvet.

Versionering ska säkerställa:

- snabb distribution av nya produkter
- korrigering av felaktig data
- stöd för framtida QR-funktioner
- stöd för framtida OCR-förbättringar
- stöd för framtida AI-funktioner

Samtidigt ska användaren kunna fortsätta använda appen fullt ut även utan internetanslutning tack vare lokal lagring i Isar.
