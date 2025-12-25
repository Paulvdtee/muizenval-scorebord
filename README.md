# 🐭 Muizenval Scorebord

Een speelse, moderne webapplicatie om muizenvangsten bij te houden op de zolder.

## ✨ Functies

- 📍 **Interactieve plattegrond** met 15 unieke muizenvallen
- 📸 **Foto upload** voor elke vangst
- 📊 **Statistieken** met overzicht van vangsten
- ✏️ **Bewerkingsmodus** om val posities aan te passen
- 💾 **Lokale opslag** - alle data blijft op je apparaat
- 📱 **Mobiel-vriendelijk** - werkt perfect op telefoon en tablet

## 🚀 Gebruik

Open `index.html` in je browser of bezoek de GitHub Pages URL.

### Op je telefoon:
1. Open de GitHub Pages link in je browser
2. Voeg toe aan je startscherm voor een app-achtige ervaring
3. Tik op een muizenval om een vangst te registreren

## 📝 Hoe te gebruiken

1. **Vangst registreren**: Tik op een muizenval op de plattegrond
2. **Foto toevoegen**: Maak een foto of kies er één uit je bibliotheek
3. **Posities aanpassen**: Klik op "Bewerken" om vallen te verplaatsen
4. **Statistieken bekijken**: Ga naar de "Stats" tab voor overzichten

## 🔥 Firebase Setup (Optioneel - voor gedeelde data)

De applicatie werkt standaard met **localStorage** (data blijft lokaal op elk apparaat). Voor **gedeelde data tussen apparaten** (bijv. jij en je vriendin zien dezelfde vangsten), kun je Firebase Realtime Database gebruiken.

### Firebase Setup Stappen:

1. **Maak een Firebase project aan:**
   - Ga naar [Firebase Console](https://console.firebase.google.com/)
   - Klik op "Add project" of "Create a project"
   - Geef je project een naam (bijv. "muizenval-scorebord")
   - Volg de wizard

2. **Activeer Realtime Database:**
   - In je Firebase project, ga naar "Realtime Database" in het linkermenu
   - Klik op "Create Database"
   - Kies "Start in test mode" (voor nu)
   - Kies een locatie (bijv. "europe-west1" voor Nederland)
   - Klik "Enable"

3. **Krijg je Firebase configuratie:**
   - Ga naar Project Settings (⚙️ icoon naast "Project Overview")
   - Scroll naar beneden naar "Your apps"
   - Klik op het web icoon (</>)
   - Geef je app een naam (bijv. "Muizenval App")
   - Kopieer de `firebaseConfig` object

4. **Voeg configuratie toe aan de app:**
   - Open `index.html` in een editor
   - Zoek naar `const firebaseConfig = {`
   - Vervang de placeholder waarden met je eigen Firebase configuratie
   - Sla het bestand op

5. **Pas database regels aan (veiligheid):**
   - Ga terug naar Realtime Database in Firebase Console
   - Klik op "Rules" tab
   - Vervang de regels met:
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
   - Klik "Publish"
   
   ⚠️ **Let op:** Deze regels maken de database publiek leesbaar/schrijfbaar. 
   
   **Voor beveiliging met authenticatie (aanbevolen):** Zie `AUTH_SETUP.md` voor instructies om alleen geautoriseerde gebruikers te laten wijzigen.

### Zonder Firebase:
Als je Firebase niet configureert, werkt de app gewoon met localStorage. Data blijft dan lokaal op elk apparaat.

## 💡 Technische details

- Pure HTML/CSS/JavaScript
- **Data opslag opties:**
  - Firebase Realtime Database (gedeeld tussen apparaten) - optioneel
  - localStorage (lokaal per apparaat) - standaard fallback
- Real-time synchronisatie wanneer Firebase is geconfigureerd
- Werkt offline (localStorage) of met real-time sync (Firebase)
- Responsive design voor alle schermformaten

## 📄 Licentie

Vrij te gebruiken voor persoonlijk gebruik.

---

Gemaakt met ❤️ voor effectieve muizenbestrijding 🐭

