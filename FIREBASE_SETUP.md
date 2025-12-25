# 🔥 Firebase Setup Instructies

## Waarom Firebase?

Firebase zorgt ervoor dat:
- ✅ Jij en je vriendin dezelfde vangsten zien
- ✅ Plattegrond posities gedeeld worden
- ✅ Real-time synchronisatie tussen apparaten
- ✅ Data wordt bewaard in de cloud (niet alleen lokaal)

## Stap-voor-stap Setup

### 1. Maak een Firebase Account
- Ga naar https://console.firebase.google.com/
- Log in met je Google account

### 2. Maak een Nieuw Project
1. Klik op "Add project" of "Create a project"
2. Geef je project een naam: `muizenval-scorebord`
3. Klik "Continue"
4. Google Analytics is optioneel - je kunt het uitzetten
5. Klik "Create project"
6. Wacht tot het project is aangemaakt, klik "Continue"

### 3. Activeer Realtime Database
1. In het linkermenu, klik op "Realtime Database"
2. Klik op "Create Database"
3. Kies "Start in test mode" (we passen de regels later aan)
4. Kies een locatie: `europe-west1` (of dichtstbijzijnde)
5. Klik "Enable"

### 4. Krijg je Configuratie Code
1. Klik op het ⚙️ (Settings) icoon naast "Project Overview"
2. Scroll naar beneden naar "Your apps"
3. Klik op het web icoon: `</>`
4. Geef je app een naam: `Muizenval App`
5. Klik "Register app"
6. **Kopieer de `firebaseConfig` object** - dit ziet er zo uit:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "muizenval-scorebord.firebaseapp.com",
  databaseURL: "https://muizenval-scorebord-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "muizenval-scorebord",
  storageBucket: "muizenval-scorebord.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

### 5. Voeg Configuratie Toe aan de App
1. Open `index.html` in een teksteditor
2. Zoek naar deze regel (rond regel 980):
   ```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       ...
   };
   ```
3. Vervang ALLE waarden met je eigen Firebase configuratie
4. Sla het bestand op

### 6. Pas Database Regels Aan
1. Ga terug naar Firebase Console
2. Klik op "Realtime Database" in het linkermenu
3. Klik op de "Rules" tab
4. Vervang de regels met:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

5. Klik "Publish"

⚠️ **Belangrijk:** Deze regels maken de database publiek toegankelijk. Voor persoonlijk gebruik is dit prima, maar voor productie gebruik zou je authenticatie moeten toevoegen.

### 7. Test de App
1. Open `index.html` in je browser
2. Open de browser console (F12)
3. Je zou moeten zien: `✅ Firebase verbonden - data wordt gedeeld tussen apparaten`
4. Test door een vangst toe te voegen
5. Open de app op een ander apparaat - de vangst zou daar ook moeten verschijnen!

## Troubleshooting

### "Firebase niet geconfigureerd" melding
- Controleer of je de configuratie correct hebt ingevuld
- Zorg dat alle velden zijn ingevuld (geen "YOUR_API_KEY" etc.)

### Data wordt niet gesynchroniseerd
- Controleer de browser console voor foutmeldingen
- Controleer of de database regels correct zijn ingesteld
- Zorg dat beide apparaten op internet zijn verbonden

### Database regels fout
- Zorg dat je de regels hebt gepubliceerd
- Controleer of `.read` en `.write` beide `true` zijn

## Kosten

Firebase Realtime Database heeft een **gratis tier** die ruim voldoende is voor persoonlijk gebruik:
- 1 GB opslag
- 10 GB downloads per maand
- 100 gelijktijdige verbindingen

Voor een muizenval tracker is dit meer dan genoeg! 🎉

## Hulp Nodig?

Als je problemen hebt:
1. Controleer de browser console voor foutmeldingen
2. Zorg dat je de laatste versie van de code hebt
3. Controleer of Firebase Realtime Database is geactiveerd

