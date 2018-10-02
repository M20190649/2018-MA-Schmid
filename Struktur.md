# Einleitung

+ Hier schonmal etwas auf das Thema der Arbeit eingehen, d.h. Fahrspurerkennung aus
    Trajektorien für Verwendung in Tracking Anwendung.
+ Ziel Erstellung von Verkehrssimulationen für Verwendung in Simulationen

## Rahmen dieser Arbeit
### Das Projekt MEC-View

+ Beschreibung des MEC View Projektes als Gesamtes (Autonomes Fahren in Innenstädten ermöglichen etc.)

### Tracking-Application

+ Beschreibung des Teilprojektes in dem diese Arbeit stattfindet. Beschreibung der Ziele, der bisherigen Möglichkeiten etc.

## Motivation und Ziele

+ Beschreibung Forschungsfragen (s. Expose)

## Aufbau der Arbeit

# Grundlagen

## Verkehranalyse aus Luftaufnahmen

+ Kurz. Grundlegende Erklärung der Möglichkeiten der Verkehrsanalyse mittels Luftaufnahmen
+ Eingehen auf die gewonnenen Roh-Video-Aufnahmen
    + Qualität
    + Szenen
    + Herausforderungen
+ Extrahierbare Kenngrößen
+ Hauptprobleme beim Arbeiten und Auswerten von Videoaufnahmen
    + Perspektivische Verzerrung
    + Ungenauigkeiten in Position und Geschwindigkeit (s. unten)
    + Occlusion

## Extraktion von Fahrzeugpositionen aus Luftaufnahmen
+ Beschreibung des Supervised-Tracking Ansatzes der im Vehicle Tracker verwendet wird (basierend auf Kaufmann Diss.)
    + *Zuvor:* Alternative Ansätze: Hintergrund-Subtraktion etc.
+ Sich hieraus ergebende Probleme (s. Supervised-Tracking mit Pixeln (Kaufmann 4.2.6))

## Verarbeitung von Fahrzeugtrajektorien

### Datenbereinigung
+ Bezug auf oben aufgeführte Probleme
+ Ansätze zur Datenbereinigung / Aufbereitung
+ Grundsätzlich: Glättung über Gleitende Lineare Regression --> Verbesserung der Positionen
+ Nicht ausreichend für Trajektorie-Analyse (hier ebenfalls Probleme):
    + Kurze Trajektorien
    + Stehende Trajektorien (vollständig (geparkte Fahrzeuge) oder teilweise (Ampeln etc.))
    + Zick-Zack aufgrund von Tracking-Fehlern

+ **WICHTIG**: Hier allgemein bleiben! Nicht mein konkretes Vorgehen beschreiben, sondern
    allgemeine Probleme, bereits durchgeführte Verbesserungen und **mögliche** weitere Verbesserungen (aus Literatur etc.). ABER: Ansätze *sollten eingesetzt werden können*
    bzw. nachher auch werden.

+ Bsp. weiter Verfahren:
    + Resampling (auf Zeitintervall oder Distanzintervall)
    + RANSAC
    + Kalman Filter

### Clusteranalyse
+ Ziel ist das Finden von Fahrspuren! Idee:
    --> Trajektorien beschreiben Bewegungsbahnen der Fahrzeuge
    --> Häufig genutzte Pfade entsprechen Fahrbahnen
    --> Gruppierung der Trajektorien um diese Pfade und daraus Fahrbahnen zu finden
+ Gruppierung der Trajektorien über Clusteranalyse
+ Beschreibung Grundlagen Clusteranalyse
+ Beschreibung der wichtigsten Verfahren / Algorithmen (Hierbei noch bezogen auf Punktmengen)
+ Grundansätze: Bottom-Up <-> Top Down
+ Eingehen auf Vor- und Nachteile
    + kMeans: Einfach, benötigt aber Anzahl Cluster
    + Spectral: performant, deterministisch(er) (Fu et al.), Basiert auf Kmeans!
    + DBScan: gute Performance, bestimmt Clusteranzahl selbst. Probleme mit unterschiedlichen
        Cluster-Dichten

#### Vergleich von Trajektorien
+ Clustering von Trajektorien: Anderes Vergleichsmaß / Distanzmaß nötig
    (Nicht simple Distanz von Punkten etc. ausreichend)
+ Einführung Grundkonzept Distanzmaße Trajektorien
+ Vorstellung der interessantesten Distanzmaße
    (Erklärung der Schwierigkeiten der Auswahl und des Vergleichs anhand der Distanzmaße)
    + HU (einfach, performant, benötigt selbe Länge der Trajektorien)
    + Hausdorff (schlechterer Perf. Vergleicht gesamte Trajektorien, Orientierung nicht berücksichtigt)
    + Mod. Hausdorff (zieht Orientierung der Trajektorien mit ein)
    + LCSS
+ Deutlich machen, dass Wahl Clustering Algo. + DM ausschlaggebend für Resultat ist

# Stand der Technik

## Clustering von Trajektoriedaten
+ Exemplarisch einige Arbeiten vorstellen (Vorgehen und Hintergrund)
+ Aufzeigen der vielen unterschiedlichen Ansätze
+ Aufzeigen der gegensätzlichen Meinungen
+ Möglichkeiten: Meist Anomaliedetektion / Szenenmodell etc.

## Definition von Fahrbahnen
+ Hierzu schon deutlich weniger Literatur
+ Unterschiedliche Ansätze
+ Unzulänglichkeiten der Ansätze (in Bezug auf die TrackerApplication)

## Klassifizierung von Fahrbahnen
+ Hier eig. keine Literatur
+ Viel zu Klassifizierung von Fahrbahnen aus Fahrzeugsicht (Kamera) --> Überholspur oder nicht
    (Fahrbahnmarkierungen)

## Benötigte Neuerungen
+ Finden eines passenden Traj. Clusterings Ansatzes für die in MEC View verwendeten Luftaufnahmen
    (häufig in Lit. auch statische Kameras etc.)
+ Extraktion von **Fahrspuren** für verschiedenste Straßentopologien nötig --> eig. nie gemacht
+ Klassifizierung auch nie gemacht

# Clustering von Fahrzeugtrajektorien

## Preprocessing
+ Bestehende Probleme (ref. Grundlagen) und gefundene / implementierte / gewählte Lösungen
+ Verendete Algorithmen
+ Konkrete Beispiele (Plots) mit Vorher-Nachher Beschreibungen des Problems

## Clustering
+ Verwendete Algos und DM
+ Probleme und gewonnene Erkenntnisse
+ Beispiele aus den verschiedenen Entwicklungsstufen Stufen
+ Probleme und deren Lösung

# Bestimmung von Fahrbahnen

+ Idealfall ohne Überschneidungen der Fahrbahnen:
    + Bestimmung Fahrbahnmittelpunkt
    + Bestimmung Fahrbahn-Begrenzungen
    + s. Vorgehen Dokument
+ Problematischer Fall von sich kreuzenden Fahrbahnen
    + Bestimmung Fahrbahnen aus Sub-Trajektorien

# Klassifizierung der Fahrbahnen

# Aufbau des LaneDetection-Moduls in TrackerApplication

# Ergebnisse und Auswertung

# Zusammenfassung und Ausblick