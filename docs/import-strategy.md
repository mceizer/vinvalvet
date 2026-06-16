Systembolaget
Producenter
Importerade CSV-filer
Manuell kurering
Användargenererade förbättringar

--------------------

Daglig import
Veckovis import
Manuell verifiering

--------------------

Producentdata vinner över OCR-data
Manuella korrigeringar vinner över importerad data

--------------------

## Distribution och lokal lagring

Vinvalvets vinindex ska distribueras som en versionssatt JSON- eller ZIP-fil.

Appen laddar ner aktuell version vid behov och importerar innehållet till lokal Isar-databas.

Sökning, OCR-matchning och QR-matchning ska i första hand ske lokalt i Isar.

Firestore ska inte användas som primär sökmotor för vinindexet, för att undvika höga läskostnader och för att appen ska fungera snabbt även offline.
