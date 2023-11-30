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


# Verständnisfragen

1. Wieso verwendet man Datenbanken?
- Große Datenmengen langfristig, effizient und ohne Fehler zu speichern
2. Was bedeuten die Abkürzungen DB und DBMS? Was versteht man unter den Begriffen und wie stehen sie zueinander in Beziehung?
- DB = Datenbank, DBMS = Datenbankmanagementsysteme
- DB ist Ort wo Daten gespeichert werden, DBMS ermöglicht Daten zu bearbeiten, löschen und neue Daten hinzuzufügen
3. Was bezeichnet man als Datenredundanz und wieso führt sie zu Problemen?
- Datenredundanz ist das mehrfache speichern von Daten (an verschiedenen Orten)
- Dies führt dazu dass beim Verändern von Daten möglicherweise nicht alle Daten verändert werden und somit Unstimmigkeiten entstehen
4. Was sind Entitäten und wie stehen sie im Verhältnis zu Entitätstypen?
5. Was sind Beziehungen und wie stehen sie im Verhältnis zu Beziehungstypen?
6. Wie werden die Eigenschaften von Entitäten ausgedrückt? Welcher Fachbegriff wird verwendet? Kennen Sie Beispiele für Eigenschaften?
7. Was ist ein Schlüssel? Wie unterscheiden sich Primär und Kandidatenschlüssel?
8. Können Beziehungen Eigenschaften enthalten? Wenn ja, kennen Sie ein Beispiel dafür?
9. Was sind die Domänen der Attribute Monat, Name, Matrikelnummer und Semesteranzahl?
10. Was sind Rollen? Wann muss man sie in ER-Diagrammen einsetzen?
11. Was versteht man unter 1:1-, 1:N- und N:M-Beziehungen?
12. Was ist das kartesische Produkt?
13. Was ist eine Relation?
14. In welchem Verhältnis stehen kartesisches Produkt und Relation?
15. Wie können Relationen dargestellt werden?

# Infos aus den Vorlesungen
## Warum werden Datenbankmanagementsysteme genutzt? 
- Reduktion der Entwicklungskosten
- Bereitstellung Mehrbenutzerbetrieb
- Vermeidung von Datenverlust
- Vermeidung von Integritätsverletzungen
- Vermeidung von Redundanzen
- Vermeidung von Integritätsverletzungen
- Beschränkungen des Datenzugriffs

## Die 9 Codd’schen Regeln
1. Integration:
einheitliche, nichtredundante Datenverwaltung
2. Operation:
Speichern, Suchen Ändern
3. Katalog:
Zugriffe auf Datenbankbeschreibungen im Data Dictionary
4. Benutzersichten:
vers. Ansichten für Admin, Nutzer
5. Integritätssicherung:
Korrektheit des Datenbankinhalts
6. Datenschutz
Ausschluss unauthorisierter Zugriffe
7. Transaktion:
mehre DB-Operationen als Funktionseinheit
8. Synchronisation
parallele Transaktionen koordinieren
9. Datensicherung
Wiederherstellung von Daten nach Systemfehlern

## Entwurf

### 1. Konzeptuelles Modell (ER-Modellierung)

- Ziel: Betrieblicher Vorgang soll durch Informationstechnik unterstützt werden
- Problem: Chaos realer Welt muss in ein *realitätsnahes* vom Computer *verarbeitbares* Modell umgesetzt werden

1. Abbildung der Situation in Form von Objekten und Beziehungen

### 2. Implementierungsschema

- Von Konzeptuelles Schema zu:
    - Relationales Schema
    - Netzwerk Schema
    - Objektorientiertes Schema

(heißt bspw.: Tabellen werden erstellt)

## Relationale Algebra und Operatorbäume

### Abarbeitung von Anfragen
1. Algebraische Vereinfachung des Terms (logische Optimierung)
2. Physische Optimierung
3. Erstellung von Kostenplänen
    1. Statistische Auswertungen (Tabellengrößen, …)
    2. Abwägung der zur Verfügung stehenden Algorithmen
4. Datenbank Tuning
