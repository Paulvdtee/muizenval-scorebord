# 🔐 Authenticatie Setup Instructies

## Overzicht

De applicatie heeft nu authenticatie toegevoegd zodat:
- ✅ **Iedereen kan bekijken** (read-only) - zonder inloggen
- ✅ **Alleen geautoriseerde gebruikers kunnen wijzigingen maken** (write) - met email/wachtwoord login
- ✅ **Bekijkmodus** - anonieme gebruikers kunnen alles zien maar niets aanpassen

## Stap 1: Activeer Firebase Authentication

1. Ga naar [Firebase Console](https://console.firebase.google.com/)
2. Selecteer je project (`muizenjacht-a7333`)
3. Klik op **Authentication** in het linkermenu
4. Klik op **Get Started** (als je dit nog niet hebt gedaan)
5. Klik op de **Sign-in method** tab
6. Klik op **Email/Password**
7. Zet de schakelaar aan voor **Enable**
8. Klik **Save**

## Stap 2: Maak Gebruikersaccounts

### Voor jezelf:
1. Ga naar **Authentication** → **Users** tab
2. Klik op **Add user**
3. Voer je email in (bijv. `jouw@email.com`)
4. Voer een tijdelijk wachtwoord in
5. Klik **Add user**
6. **Belangrijk:** Stuur jezelf een wachtwoord reset email of verander het wachtwoord later

### Voor je vriendin:
1. Herhaal bovenstaande stappen met haar email
2. Of laat haar zichzelf registreren via de app (zie Stap 3)

## Stap 3: Activeer Gebruikersregistratie (Optioneel)

Als je wilt dat gebruikers zichzelf kunnen registreren:

1. Ga naar **Authentication** → **Sign-in method**
2. Klik op **Email/Password**
3. Zet ook **Email link (passwordless sign-in)** aan (optioneel)
4. Klik **Save**

Nu kunnen nieuwe gebruikers zichzelf registreren via de login modal.

## Stap 4: Pas Database Regels Aan

Dit is **cruciaal** voor de beveiliging!

1. Ga naar **Realtime Database** in Firebase Console
2. Klik op de **Rules** tab
3. Vervang de regels met:

```json
{
  "rules": {
    ".read": true,
    ".write": "auth != null && auth.token.firebase.sign_in_provider != 'anonymous'"
  }
}
```

**Uitleg:**
- `.read: true` - Iedereen kan lezen (ook zonder login)
- `.write: "auth != null && !auth.token.firebase.sign_in_provider === 'anonymous'"` - Alleen ingelogde gebruikers (niet anoniem) kunnen schrijven

4. Klik **Publish**

## Stap 5: Activeer Anonieme Authenticatie (Voor Bekijkmodus)

1. Ga naar **Authentication** → **Sign-in method**
2. Klik op **Anonymous**
3. Zet de schakelaar aan voor **Enable**
4. Klik **Save**

Dit maakt de "Bekijken zonder inloggen" functie mogelijk.

## Stap 6: Test de Applicatie

1. Open de applicatie in je browser
2. Je ziet een login modal
3. Test **"Bekijken zonder inloggen"**:
   - Klik op de knop
   - Je kunt nu alles bekijken maar niets aanpassen
   - Geen "Bewerken" knop zichtbaar
   - Geen delete buttons bij vangsten

4. Test **Inloggen**:
   - Klik op "Inloggen"
   - Voer je email en wachtwoord in
   - Je ziet nu je email in de header
   - "Bewerken" knop is zichtbaar
   - Je kunt vangsten toevoegen en verwijderen

## Gebruikersbeheer

### Gebruikers bekijken:
- Ga naar **Authentication** → **Users** tab
- Hier zie je alle geregistreerde gebruikers

### Gebruiker verwijderen:
- Klik op de drie puntjes naast een gebruiker
- Kies **Delete user**

### Wachtwoord resetten:
- Gebruikers kunnen zelf hun wachtwoord resetten via de login modal (als je email link hebt ingeschakeld)
- Of jij kunt het wachtwoord resetten via de Firebase Console

## Veiligheid

### Best Practices:
1. ✅ Gebruik sterke wachtwoorden
2. ✅ Deel je login gegevens alleen met vertrouwde personen
3. ✅ Controleer regelmatig de gebruikerslijst
4. ✅ Houd de database rules up-to-date

### Database Rules Uitleg:
- **Read: true** - Iedereen kan de data lezen (nodig voor publieke weergave)
- **Write: authenticated only** - Alleen ingelogde gebruikers kunnen schrijven
- **Anonymous users excluded** - Anonieme gebruikers kunnen niet schrijven

## Troubleshooting

### "Permission denied" fout bij opslaan
- Controleer of je bent ingelogd (niet anoniem)
- Controleer of de database rules correct zijn gepubliceerd
- Controleer of Email/Password authenticatie is ingeschakeld

### Login werkt niet
- Controleer of Email/Password authenticatie is ingeschakeld
- Controleer of de gebruiker bestaat in Firebase Console
- Controleer of het wachtwoord correct is

### Anonieme login werkt niet
- Controleer of Anonymous authenticatie is ingeschakeld
- Controleer de browser console voor foutmeldingen

### Gebruikers kunnen zich niet registreren
- Controleer of gebruikersregistratie is ingeschakeld in Firebase
- Controleer of Email/Password authenticatie is ingeschakeld

## Kosten

Firebase Authentication heeft een **gratis tier**:
- Tot 50.000 MAU (Monthly Active Users)
- Onbeperkte verificaties
- Alle standaard authenticatie methoden

Voor persoonlijk gebruik is dit meer dan genoeg! 🎉

