# Piano di Studio Interattivo

Web app statica pronta per GitHub Pages, installabile sul telefono e con sincronizzazione cloud opzionale tramite Firebase.

## Pubblicazione su GitHub Pages

1. Crea un repository GitHub.
2. Carica questi file nella root del repository:
   - `index.html`
   - `manifest.webmanifest`
   - `service-worker.js`
   - `icon.svg`
   - `firebase-config.js`
3. Vai su `Settings > Pages`.
4. In `Build and deployment`, scegli `Deploy from a branch`.
5. Seleziona branch `main` e cartella `/root`.

## Sincronizzazione tra dispositivi

GitHub Pages ospita la web app, ma non salva dati condivisi. Per sincronizzare telefono e computer serve Firebase.

1. Crea un progetto su Firebase.
2. Aggiungi una Web App da `Project settings > Your apps`.
3. Copia la configurazione Firebase dentro `firebase-config.js`.
4. Attiva `Authentication > Sign-in method > Anonymous`.
5. Attiva `Firestore Database`.
6. Imposta regole Firestore adatte a un uso personale.

Esempio semplice per uso personale durante i test:

```txt
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /studyPlans/{document} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Con questa configurazione ogni dispositivo collegato alla stessa pagina userà il documento `studyPlans/main`.
