# Come pubblicare una nuova versione di Magazzino De Pio

Passi da ripetere per ogni aggiornamento. Tutto è gratuito (repository pubblico e Release su GitHub, senza carta).

L'app controlla questo indirizzo:

`https://raw.githubusercontent.com/remcaldaie-art/depio-magazzino-updates/main/version.json`

Se `versionCode` è più alto di quello installato, l'utente può scaricare e installare l'APK.

## 1. Costruire l'APK

- Alzare `versionCode` e `versionName` (es. 30 / 1.30).
- Firmare con `depio-release.keystore` (la stessa di sempre; una firma diversa non si installa sopra).
- File di uscita: `/workspace/DePioMagazzino-vNN.apk` (es. `DePioMagazzino-v30.apk`).

## 2. Aggiornare version.json

Nel file `version.json` del ramo `main`:

```json
{
  "versionCode": 30,
  "versionName": "1.30",
  "apkUrl": "https://github.com/remcaldaie-art/depio-magazzino-updates/releases/download/1.30/DePioMagazzino-v30.apk",
  "notes": "Breve descrizione della versione"
}
```

Il nome del file in `apkUrl` deve coincidere esattamente con l'allegato della Release.

## 3. Caricare i file sul ramo main

```bash
cd /workspace/depio-updates
git add version.json README.md HOWTO-PUBLISH.md
git commit -m "Versione 1.30"
git push origin main
```

## 4. Creare la Release e allegare l'APK

```bash
gh release create 1.30 /workspace/DePioMagazzino-v30.apk \
  --repo remcaldaie-art/depio-magazzino-updates \
  --title "1.30" \
  --notes "Breve descrizione della versione"
```

Il tag (es. `1.30`) deve essere uguale a `versionName`. L'allegato deve chiamarsi come in `apkUrl` (es. `DePioMagazzino-v30.apk`).

## 5. Verificare

```bash
curl -fsSL https://raw.githubusercontent.com/remcaldaie-art/depio-magazzino-updates/main/version.json
curl -fsSL -L -o /tmp/check.apk \
  https://github.com/remcaldaie-art/depio-magazzino-updates/releases/download/1.30/DePioMagazzino-v30.apk
sha256sum /tmp/check.apk
```

Controllare che `versionCode` sia quello nuovo e che lo SHA-256 coincida con l'APK firmato.

## Note

- Non mettere l'APK nel repository git: va solo come allegato della Release.
- Non usare funzioni a pagamento di GitHub.
- I dati in magazzino sull'app restano all'aggiornamento.
