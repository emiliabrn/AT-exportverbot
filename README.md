# Exportverbot-Monitor Österreich

Täglicher Abgleich der BASG-Exportverbotsliste. Bei Änderungen: E-Mail. Immer: Webseite unter GitHub Pages.

## Einrichtung (ca. 10 Minuten)
1. Neues GitHub-Repository anlegen (privat oder öffentlich) und diese Dateien hochladen.
2. Settings → Pages → Source: "Deploy from a branch", Branch `main`, Ordner `/docs`.
3. Settings → Secrets and variables → Actions → **Secrets**: `SMTP_HOST`, `SMTP_PORT` (587), `SMTP_USER`, `SMTP_PASS`, `MAIL_TO`, optional `MAIL_FROM`.
   (Gmail: App-Passwort verwenden, Host `smtp.gmail.com`.)
   Optional unter **Variables**: `PAGE_URL` = Adresse deiner Pages-Seite (kommt in die Mail).
4. Actions → "Exportverbot-Monitor" → "Run workflow". Der erste Lauf speichert nur den Basisstand (keine Mail).

## Falls der erste Lauf scheitert
Die BASG-Seite ist eine JS-App. Das Skript greift deren JSON-Antworten automatisch ab, sonst liest es die Tabelle.
Bei Fehlern: Artefakt "debug" aus dem Actions-Lauf herunterladen (response_*.json, page.png) und die Feldnamen anpassen.

## Lokal testen
pip install -r requirements.txt && playwright install chromium
python monitor.py --debug --no-mail
