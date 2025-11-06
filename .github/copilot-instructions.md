## Kurz & bündig — Ziel für KI-Coder

Dieses Repository ist ein VS Code Extension Pack (Docker). Ziel: Hilf Entwickler*innen schnell produktiv zu werden, indem du präzise Änderungen vorschlägst, die zu den vorhandenen Konventionen passen.

### Wichtige Fakten (Big picture)
- Art: VS Code Extension Pack / Extension (kein monorepo, enthält Ressourcen und Metadaten).
- Entry points: `package.json` (Extension manifest / metadata). Schau hier für Abhängigkeiten (`extensionDependencies`) und Packaging-Script (`scripts.package`).
- Assets: `resources/` (Screenshots, GIFs, walkthroughs) — verändere Pfade nur wenn du alle Verweise anpasst.
- CI: `.github/workflows/*` (Workflow-Logik live im Repo).

### Wichtige Dateien, die du referenzierst
- `README.md` — Projektüberblick und Contributing-Hinweise.
- `package.json` — metadata, `scripts` (z.B. `package: vsce package`).
- `resources/readme/*` und `resources/walkthroughs/*` — UI-Bilder und GIFs, werden in README/Wiki benutzt.
- `.github/workflows/*.yml` — CI/automation patterns (prüfe sie vor Änderungen an Build-/Publish-Schritten).

### Entwickler-Workflows / Befehle
- Packaging: `vsce package` (ist als `scripts.package` eingetragen). Verwende diesen Befehl, wenn du ein .vsix erzeugen musst.
- Build/Test: Es gibt aktuell keine `build`/`test`-Skripte in `package.json`. Schreibe keine Änderungen voraus, die neue Toolchains erfordern, ohne das Team zu fragen.

### Projekt-spezifische Konventionen
- Keine komplizierte Build-Pipeline: Änderungen an der Extension sollten Dateien in `resources/` und `package.json` betreffen; vermeide das Hinzufügen schwergewichtiger Build-Tools ohne Abstimmung.
- Assets: GIF/PNG-Dateien in `resources/` sind Teil der Dokumentation — optimiere nur, wenn du die Qualität/Größe kontrollierst.
- Backwards compatibility: Diese Extension-Pack-Manifeständerungen können Einfluss auf marketplace-Publishing haben (version/publisher). Passe `version` nur wenn du bewusst packagest.

### Beispiele (konkrete Patterns aus dem Repo)
- Packaging-Eintrag: `"package": "vsce package"` → benutze `vsce` für Release/Pack.
- Extension-Dependency: `"extensionDependencies": ["ms-azuretools.vscode-containers"]` → wenn du Funktionalität entfernst, prüfe ob die dependency noch nötig ist.
- Walkthroughs: `resources/walkthroughs/1g-addDockerFiles.gif` → wenn du Pfad änderst, update README und alle Referenzen.

### Sicherheits- & Policy-Hinweise
- Keine Secrets ins Repo einfügen. CI arbeitet in `.github/workflows/`; wenn ein Secret benötigt wird, signalisiere dies im PR und verweise auf die org-Secret-Mechanik.

### Was KI-Vorschläge vermeiden sollten
- Automatisches Hinzufügen umfassender Build-Stacks (Webpack, TypeScript-Tooling) ohne explizite Hinweise im Issue/PR.
- Entfernen oder Umbenennen von Ressourcen ohne Update aller Referenzen (`README.md`, workflows, Marketplace-Links).

Wenn du unsicher bist, füge in den PR eine klare Beschreibung, warum die Änderung nötig ist, welche Files betroffen sind, und: "Small, reversible"-Commits bevorzugt. Frage nach, wenn Build/Test-Befehle ergänzt werden sollen.

---
Bitte sag mir, welche Bereiche du genauer möchtest (z. B. CI-Analyse, Packaging-Workflow, oder automatische Tests hinzufügen) — ich passe die Instruktion an.
