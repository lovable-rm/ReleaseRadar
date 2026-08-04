# Release Radar auf Vercel

## Bereitstellen

1. Diesen Ordner in ein GitHub-Repository hochladen.
2. In Vercel **Add New → Project** wählen.
3. Das GitHub-Repository importieren.
4. Als Framework **Other** verwenden.
5. Build Command leer lassen und als Output Directory `.` verwenden.
6. **Deploy** auswählen.

Die Startseite liegt in `index.html`. Die aktuellen Einträge stehen in
`releases.json` und werden bei jedem Seitenaufruf ohne Browser-Cache geladen.

## Daten aktualisieren

Neue Releases werden ausschließlich in `releases.json` ergänzt. Der
eingebettete Datenstand in `index.html` dient als Ausfallsicherung.

Vercel aktualisiert diese Datei nicht selbstständig. Bei einer
GitHub-basierten Bereitstellung veröffentlicht Vercel automatisch jeden neuen
Commit. Für eine tägliche Aktualisierung muss daher zusätzlich ein geplanter
Job die Quellen prüfen, `releases.json` ändern und die Änderung in das
GitHub-Repository übertragen.

Der empfohlene Ablauf ist:

1. Outlook, Teams, Jira sowie App Store und Google Play prüfen.
2. Neue Einträge anhand ihrer stabilen Quell-ID mit den vorhandenen Einträgen
   abgleichen.
3. `releases.json` aktualisieren und committen.
4. Vercel übernimmt den Commit und stellt die neue Version bereit.

Ohne den geplanten Schreibzugriff auf das GitHub-Repository bleibt die Website
auf dem zuletzt veröffentlichten Stand.

`robots.txt`, der HTML-Meta-Tag und der `X-Robots-Tag` verhindern die
Indexierung durch kooperative Suchmaschinen. Die Website ist dadurch nicht
privat; wer die URL kennt, kann sie aufrufen.
