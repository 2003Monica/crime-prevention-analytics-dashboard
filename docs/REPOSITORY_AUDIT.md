# Repository audit

## Scope

This repository is the extracted package content of a Power BI `.pbix` report. The audit preserves the generated package layout and report logic.

## Findings

- **Duplicates:** SHA-256 comparison found no files with identical content.
- **Unused static resources:** None identified. Each file under `Report/StaticResources/RegisteredResources/` is referenced by at least one report definition.
- **Generated local state:** `DAXQueries/.pbi/daxQueries.json` is Power BI Desktop state. It is currently tracked, but future `.pbi` content is ignored. Removing an already-tracked package file was avoided because its effect on the extracted artifact was not verified.
- **DAX query file:** `DAXQueries/Query%201.dax` contains a Power BI query-view document with report measures and Microsoft's default introductory comments. It was retained because it documents implemented calculations.
- **Credentials:** No hard-coded passwords, API keys, bearer tokens, client secrets, or private keys were found in text-searchable content.
- **Connection metadata:** `Connections` contains dataset and report GUIDs only. These IDs are not credentials, but owners may choose to omit them if they do not want workspace artifact identifiers published.
- **Binary model:** `DataModel` is a binary semantic model containing embedded data. Automated text scanning cannot prove the absence of sensitive values inside a binary model. Review the model's data classifications and licensing before publishing.
- **Code comments:** No hand-written source modules are present. Generated Power BI JSON was not annotated because comments would make JSON invalid and could break the report.

## Public GitHub checklist

- Confirm that the embedded data may be redistributed publicly.
- Confirm that all included imagery and theme resources may be redistributed.
- Consider Git LFS if repository hosting limits become an issue for `DataModel`.
- Add a license only after the project owner selects one and confirms rights to the data and assets.
- Re-run secret scanning after future data-source or connection changes.

