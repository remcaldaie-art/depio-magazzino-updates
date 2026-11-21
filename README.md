# Aggiornamenti Magazzino De Pio

Repository pubblico per gli aggiornamenti dell'app **Magazzino De Pio** (`it.depio.magazzino`).

L'app, all'avvio (se c'è internet) e quando si tocca **Aggiorna app**, legge questo file:

`https://raw.githubusercontent.com/remcaldaie-art/depio-magazzino-updates/main/version.json`

Se `versionCode` è più alto di quello installato, compare il banner arancione e si può scaricare l'APK. L'utente tocca **Installa**. I dati in magazzino restano.

## Contenuto di version.json

```json
{
  "versionCode": 29,
  "versionName": "1.29",
  "apkUrl": "https://github.com/remcaldaie-art/depio-magazzino-updates/releases/download/1.29/DePioMagazzino-v29.apk",
  "notes": "Breve descrizione della versione"
}
```

## Come pubblicare una nuova versione

1. Costruire l'APK firmata con `depio-release.keystore` (stessa firma delle versioni precedenti, altrimenti l'aggiornamento non si installa sopra).
2. Aggiornare `version.json` con il nuovo `versionCode`, `versionName`, `apkUrl` e `notes`.
3. Caricare `version.json` sul ramo `main`.
4. Creare una GitHub Release con tag uguale al `versionName` (es. `1.29`) e allegare l'APK con lo stesso nome indicato in `apkUrl` (es. `DePioMagazzino-v29.apk`).

Repo previsto: `remcaldaie-art/depio-magazzino-updates` (pubblico).
