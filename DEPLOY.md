# Deployment auf GitHub Pages – Schritt für Schritt

## 1. GitHub-Repository erstellen

1. Gehe zu https://github.com/new
2. Repository-Name: `it-notfallkontakte`
3. Sichtbarkeit: **Public** (nötig für kostenloses GitHub Pages)
4. Erstellen klicken

## 2. Code hochladen

```bash
cd ~/Desktop/QR_AO_4_Kontakte
git init
git add index.html vcf/ qr-code.png qr-code.svg CLAUDE.md
git commit -m "IT-Notfallkontakte Landing Page"
git branch -M main
git remote add origin https://github.com/DEIN-USERNAME/it-notfallkontakte.git
git push -u origin main
```

## 3. GitHub Pages aktivieren

1. Im Repository → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / `/ (root)`
4. **Save** klicken
5. Nach 1-2 Minuten live unter: `https://DEIN-USERNAME.github.io/it-notfallkontakte/`

## 4. QR-Code aktualisieren (falls nötig)

Wenn dein GitHub-Username nicht `niklasnengelken` ist, muss der QR-Code neu generiert werden. Siehe Anleitung in CLAUDE.md.

## 5. Testen

- **iPhone**: QR-Code scannen → Seite öffnet → einzelne Kontakte antippen → Kontakte-App öffnet sich → Speichern
- **Android**: QR-Code scannen → "Alle 4 Kontakte speichern" → `.vcf`-Datei wird heruntergeladen → alle 4 Kontakte importiert
- **Desktop/Mac**: Gleich wie Android

## MIME-Type Hinweis

GitHub Pages liefert `.vcf`-Dateien automatisch mit dem richtigen `text/vcard` MIME-Type aus. Kein extra Setup nötig.
