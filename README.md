# Datenbanken Klausur Cheatsheet


# Ocean Tutorial
1. Go to https://ocean.f4.htw-berlin.de/
2. Login mit Matrikelnummer + Passwort
3. Neue Datenbank erstellen
4. Auf "Adminer" klicken, führt zu psql.f4.htw-berlin.de

   - Datenbank System  = PostgreSQL
   - Server            = Link kopieren aus Ocean 
   - Benutzer          = Matrikelnr (mit s0)
   - Passwort          = htw passwort
   - Database          = Name der Datenbank

# Useful Links

- https://wikis.gm.fh-koeln.de/Datenbanken/Relationale-Algebra
- https://www.cs.hs-rm.de/~knauf/Datenbanken2018/Vorlesung5.pdf
- https://www.w3schools.com/sql/default.asp

- https://quizlet.com/de/karteikarten/datenbanksystem-412568469

# Beispiel SQL Abfragen (mit seiner Datenbank)

- Wie viele Kilometer ist Dieter Doping insgesamt gefahren?

SELECT SUM(km)FROM mitglieder, faehrt, strecken
WHERE mitglieder.nummer = 4 AND faehrt.fahrer = mitglieder.nummer AND faehrt.strecke = strecken.name
- Wie viel Durchschnittswatt hatten Leute die "48 Kehren in toller Landschaft" gefahren sind?

SELECT durchschnittwatt FROM faehrt, strecken
WHERE  strecken.beschreibung = '48 Kehren in toller Landschaft' AND strecken.name = faehrt.strecke
- Welcher Fahrer kann Rekorde brechen?

SELECT DISTINCT mitglieder.name FROM mitglieder, faehrt, kategorien, strecken
WHERE  kategorien.name = 'Flachland' AND kategorien.name = strecken.kat AND strecken.name = faehrt.strecke AND mitglieder.nummer = faehrt.fahrer
- Wie viel Watt hat CQ in der Hölle  verbraten?

SELECT SUM(durchschnittwatt) FROM faehrt, strecken, mitglieder
WHERE strecken.name = 'Mont Ventoux' AND strecken.name = faehrt.strecke AND faehrt.fahrer = mitglieder.nummer AND mitglieder.name = 'Carsten Quäler'
- Welcher Fahrer hatte ein Frequenz von 72?

SELECT DISTINCT mitglieder.name FROM faehrt, strecken, mitglieder
WHERE  faehrt.fahrer = mitglieder.nummer AND  faehrt.durchschnitttrittfrequenz = 72
