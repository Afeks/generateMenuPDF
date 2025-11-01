# Setup-Anleitung für separates Repository

## Repository auf GitHub erstellen

1. Gehe zu GitHub und erstelle ein neues Repository (z.B. `associationWebCat-functions`)
2. **Wichtig:** Erstelle das Repository **ohne** README, .gitignore oder LICENSE (diese sind bereits vorhanden)

## Repository verbinden und pushen

```bash
cd /Users/felix/Development/associationWebCat-functions

# Remote Repository hinzufügen (ersetze USERNAME und REPO_NAME)
git remote add origin https://github.com/USERNAME/associationWebCat-functions.git

# Branch umbenennen (falls nötig)
git branch -M main

# Code hochladen
git push -u origin main
```

## Firebase-Konfiguration

Nach dem Verschieben in ein separates Repository muss Firebase neu konfiguriert werden:

```bash
cd /Users/felix/Development/associationWebCat-functions

# Firebase Login (falls noch nicht geschehen)
firebase login

# Projekt auswählen oder hinzufügen
firebase use --add
# Wähle das Projekt: arp-test-14a84

# Verifiziere die Konfiguration
firebase projects:list
```

Die `firebase.json` in diesem Repository ist bereits konfiguriert mit `"source": "."` (aktuelles Verzeichnis statt "functions").

## Dependencies installieren

```bash
npm install
```

## Deployment

```bash
# Alle Functions deployen
firebase deploy --only functions

# Oder nur eine Function
firebase deploy --only functions:generateMenuPDF
```

## Haupt-Repository aktualisieren

Nach dem Verschieben müssen Sie im Haupt-Repository (`associationWebCat`):

1. Das `functions/` Verzeichnis entfernen oder durch ein Git Submodule ersetzen
2. Die `firebase.json` im Haupt-Repository anpassen, falls nötig

### Option 1: Functions als Git Submodule (empfohlen)

```bash
cd /Users/felix/Development/associationWebCat

# Altes functions-Verzeichnis entfernen
rm -rf functions

# Als Submodule hinzufügen
git submodule add https://github.com/USERNAME/associationWebCat-functions.git functions
```

### Option 2: Functions-Verzeichnis entfernen

Falls Sie die Functions nicht mehr im Haupt-Repository benötigen:

```bash
cd /Users/felix/Development/associationWebCat

# Aus Git entfernen
git rm -r functions

# Lokales Verzeichnis entfernen (optional)
rm -rf functions
```

**Wichtig:** Die `firebase.json` im Haupt-Repository muss dann angepasst werden, um auf das separate Repository zu verweisen, oder Sie deployen die Functions direkt aus dem neuen Repository.

