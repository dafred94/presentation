# Studentenprojekte bei Frederic Bruder

(diese Seite am besten im neuen Tab ansehen unter https://github.com/dafred94/presentation#readme )

... zuerst eine kleine Einführung in mein Gebiet. Andere Vorschläge bzw. Themen weiter unten!

## Hauptforschungsgebiet: Grey Box Modeling

Physikalische Simulationsmodelle sollen verbessert werden.. mit AI-Methoden.

Bilder sagen mehr als 1000 Worte.
Diese hier nicht wirklich, geben aber einen "Eindruck" von dem, was passiert.

### Das Szenario

Ein System soll modelliert werden. Also zB eine Schaukel.
Die Schaukel wird auf unterschiedliche Art und Weise angestoßen, Daten werden dann als Zeitreihen (provided data) gemessen.

### white box Modellierung

Wir schlagen ein Physikbuch auf und finden die Differentialgleichungen für einen reibungsfreien Oszillator.
Hier auch als "Pendel" bekannt.
Nun kennen wir die Parameter des "Pendels" aber nicht.

Was nun? Hier probieren wir, die Parameter des Oszillators (model) zu optimieren:

https://user-images.githubusercontent.com/53007095/167388204-fb2ad500-76de-4af6-9dbf-4baac0b40996.mp4

Geht irgendwie in die richtige Richtung.. Aber der reibunsfreie Oszillator hält immer an seiner Amplitude fest.
Das wollen wir so nicht und schreiben deshalb einfach mal einen linearen Reibungterm ins Modell.

Auch jetzt optimieren wir wieder die Parameter:

https://user-images.githubusercontent.com/53007095/167388570-ee48f873-e2fa-4c46-a87c-4e49c6ea0693.mp4

Das Ergebnis sieht schon besser aus! Amplitude geht runter. Aber zu schnell!

Nun könnten wir weiter und weiter beliebige Terme hinzufügen, bis uns das Ergebnis passt.

... Oder wir versuchen uns an

### Grey Box Modellierung

Kurz und knapp: wirf ein neurales Netzwerk auf das Problem!
Aber nicht unbedingt ein rekurrentes, bei dem wir nicht mehr verstehen, was zwischen den Zeitschritten passiert.
Sondern einen Regressor innerhalb der Differentialgleichug des Oszillators!

https://user-images.githubusercontent.com/53007095/167390440-de463cf5-df7c-4f95-8b9e-21dfe4649c9d.mp4

Sieht noch etwas besser aus! Aber schon das Training dauerte eine gefühte Ewigkeit. Hier ist also noch viel Platz nach oben.

Wichtige Fragestellungen:
- Wir trainieren wir solche Modelle am besten?
- Was macht sie genau, was macht sie in der Ausführung schnell?
- Wie genau bauen wir sie auf? In unserem Schaukelmodell wurde der Beschleunigungsterm verändert. Wo packen wir in größeren Modellen an?

## weitere Vorschläge

### Übersetzung von Modelica/GALEC zu Julia zur Unterstützung der Entwicklung von Grey Box Modellen
- in der Industrie ist Modelica eine verbreitete Sprache zur akausalen (gleichungsbasierten) Systemmodellierung
- Problem: die kausalisierten Modelle kriegt man (bequem) meist nur als FMUs aus den Modelica-Tools wie Dymola heraus. Diese FMUs beinhalten kompilierten Code zur Berechnung der Zustandsableitung der Modelle.
- Es ist aber nicht mehr direkt möglich, die kausalisierten Modelle auf Zuweisungsebene zu manipulieren. Damit ist man bei der Erstellung von NeuralODEs leider ziemlich eingeschränkt.
- GALEC-Code ist ein neuer Teil der eFMI-Spezifikation https://emphysis.github.io/pages/downloads/efmi_specification_1.0.0-alpha.4.html#AlgorithmCode
neue Versionen von Modelica-Tools können kausalisierte Modelle in dieser Form exportieren
- **was wir brauchen**
  - einen Übersetzer von GALEC-Code zur Julia, damit uns der Modellcode in Julia vorliegt.
  - oder **alternativ** ein Interface zwischen dem Output von `OMParser.jl` und Julia-basierten Simulationstools wie `Modia` oder `ModelingToolkit.jl`
- das Thema ist eher **programmiersprachenlastig**, man sollte also grob verstehen wie Parser und Übersetzer funktionieren
- Erfahrung mit ANTLR wäre von Vorteil

### Weiterentwicklung eines interaktiven Quadcoptermodells
- für eine Lehrveranstaltung wurde bereits ein simples Simulationsmodell eines Quadcopters in Julia erstellt
- dieses soll verfeinert werden
  - die Rotation soll von Eulerwinkeln auf Quaternions umgestellt werden, um Singularitäten bzw. extrem steife Differentialgleichungen zugunsten der Echtzeitsimulation zu vermeiden
  - der Quadcopter soll geregelt werden, sodass man ihn mit einem Gamepad in virtueller Umgebung steuern kann
  - Integration weiterer physikalischer Effekte (Akkudynamik, Gyroskopische Effekte der Rotoren...)
  - ...
- weitere, gerne auch verrückte, Ideen sind willkommen. Das Ziel ist einen attraktiven und gut dokumentierten Demonstrator zu haben!
  - Ausbau zur Drone Racing Simulation ???
- das Thema ist **mechanik- und regelungstechniklastig**
- es hat gewisse Überschneidungen mit **Spieleentwicklung** (Interaktion, virtuelle Umgebung, Rendering)

