# Association Web Cat - Cloud Functions

Dieses Repository enthält die Firebase Cloud Functions für Association Web Cat.

## Funktionen

### `generateMenuPDF`

Generiert PDFs aus HTML für den MenuDesigner. Jede Servierstelle erhält eine eigene A4-Seite mit individuellen QR-Codes.

**Endpoint:** `POST https://europe-west1-{projectId}.cloudfunctions.net/generateMenuPDF`

**Request Body:**
```json
{
  "html": "<html>...</html>",
  "options": {}
}
```

**Response:** PDF-Datei als Binary

## Setup

### Voraussetzungen

- Node.js 20
- Firebase CLI (`npm install -g firebase-tools`)
- Firebase-Projekt konfiguriert

### Installation

```bash
npm install
```

### Lokale Entwicklung

```bash
# Firebase Emulator starten
npm run serve

# Oder direkt mit Firebase CLI
firebase emulators:start --only functions
```

### Deployment

```bash
# Einzelne Function deployen
firebase deploy --only functions:generateMenuPDF

# Alle Functions deployen
firebase deploy --only functions
```

## Projekt-Struktur

```
.
├── src/
│   └── index.js          # Haupt-Functions-Code
├── package.json           # Dependencies
├── .gitignore            # Git ignore rules
└── README.md             # Diese Datei
```

## Firebase-Konfiguration

Dieses Repository ist als separates Projekt konfiguriert. Um es mit Firebase zu verbinden:

1. Erstelle ein neues Firebase-Projekt oder verknüpfe es mit einem bestehenden
2. Führe `firebase login` aus
3. Führe `firebase use --add` aus, um das Projekt auszuwählen
4. Erstelle eine `firebase.json`:

```json
{
  "functions": {
    "source": ".",
    "runtime": "nodejs20"
  }
}
```

## Abhängigkeiten

- `firebase-admin`: Firebase Admin SDK
- `firebase-functions`: Firebase Functions SDK
- `puppeteer-core`: Headless Browser für PDF-Generierung
- `@sparticuz/chromium`: Optimiertes Chromium für Serverless
- `pdf-lib`: PDF-Manipulation und Zusammenführung

## Lizenz

Teil von Association Web Cat
