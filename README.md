# Forschungsgebiet Frederic Bruder

Physikalische Simulationsmodelle sollen verbessert werden.. mit AI-Methoden.

Bilder sagen mehr als 1000 Worte.
Diese hier nicht wirklich, geben aber einen "Eindruck" von dem, was passiert.

## Das Szenario

Ein System soll modelliert werden. Also zB eine Schaukel.
Die Schaukel wird auf unterschiedliche Art und Weise angestoßen, Daten werden dann als Zeitreihen (provided data) gemessen.

## white box Modellierung

Wir schlagen ein Physikbuch auf und finden die Differentialgleichungen für einen reibungsfreien Oszillator.
Hier auch als "Pendel" bekannt.
Nun kennen wir die Parameter des "Pendels" aber nicht.

Was nun? Hier probieren wir, die Parameter des Oszillators (model) zu optimieren:

![](wb_model.webm?raw=true)

Geht irgendwie in die richtige Richtung.. Aber der reibunsfreie Oszillator hält immer an seiner Amplitude fest.
Das wollen wir so nicht und schreiben deshalb einfach mal einen linearen Reibungterm ins Modell.

Auch jetzt optimieren wir wieder die Parameter:

![](wb_lin_friction.gif?raw=true)

Das Ergebnis sieht schon besser aus! Amplitude geht runter. Aber zu schnell!

Nun könnten wir weiter und weiter beliebige Terme hinzufügen, bis uns das Ergebnis passt.

... Oder wir versuchen uns an

## Grey Box Modellierung

Kurz und knapp: wirf ein neurales Netzwerk auf das Problem!
Aber nicht unbedingt ein rekurrentes, bei dem wir nicht mehr verstehen, was zwischen den Zeitschritten passiert.
Sondern einen Regressor innerhalb der Differentialgleichug des Oszillators!

![](out.gif?raw=true)

Sieht noch etwas besser aus! Aber schon das Training dauerte eine gefühte Ewigkeit. Hier ist also noch viel Platz nach oben.

Wichtige Fragestellungen:

Wir trainieren wir solche Modelle am besten?

Was macht sie genau, was macht sie in der Ausführung schnell?

Wie genau bauen wir sie auf? In unserem Schaukelmodell wurde der Beschleunigungsterm verändert. Wo packen wir in größeren Modellen an?
