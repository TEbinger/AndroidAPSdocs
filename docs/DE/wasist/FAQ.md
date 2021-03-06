# FAQ für Looper

So kannst du die FAQ ergänzen: [Anleitung](https://androidaps.readthedocs.io/en/latest/DE/mithelfen/wiki.html).

Wenn du deine Frage nicht gefunden hast, findest du sie vielleicht in den [Englischen FAQ](http://androidaps.readthedocs.io/en/latest/EN/Getting-Started/FAQ.html).

## Allgemeines

### Wie fange ich an?
Die wichtigste Voraussetzung für den closed Loop ist, dass deine Basalrate und Faktoren genau sind. Die Einstellungen die der Loop für dich machen kann sind sicherheitshalber begrenzt (siehe maximal erlaubte temporäre [Basalrate](https://openaps.org/reference-design/)), das heißt, dass du die vorhandenen Ressourcen nicht für eine schlecht eingestellte Basalrate verschwenden solltest. Falls der Loop z.B. vor dem Essen immer die Insulinzufuhr zurück dreht, heißt das höchstwahrscheinlich, dass du die Basalrate anpassen musst. Du kannst [autotune](https://openaps.readthedocs.io/en/latest/docs/walkthrough/phase-4/autotune.html) verwenden um deine Daten zu analysieren, und Vorschläge zur Änderung der Basalrate/Faktoren zu bekommen (Jedoch mit Vorsicht zu genießen, das System kann z.B. nicht unterscheiden, ob du wegen Sport zu niedrig wurdest, oder ob die Basalrate nicht passt), oder du kannst deine Basalrate mit einem "altmodischen" Basalratentest testen.

### Wo gibt es Hilfestellungen beim Loopen?

* Falls du nicht möchtest, dass man die Einstellungen einfach ändert, kannst du im Preferences Menü ein Passwort einstellen. Wenn du dann das nächste mal in das Preferences Menü gehst, wirst du zuerst aufgefordert das Passwort einzugeben, bevor du irgendwelche Einstellungen vornehmen kannst. Falls du die Option wieder deaktivieren möchtest, gehe zu "password for settings" und lösche die Zeichen.
* Wenn du die Android Wear App verwenden möchtest, achte darauf, dass AndroidAPS Benachrichtigungen auf der Uhr anzeigen darf. Siehe auch [Details zu den Watch Faces](./Watchfaces)
* Wenn du die Pumpe mal abnimmst, drücke und halte im Hauptmenü den "Closed Loop" Text und wähle anschließend "Trenne Pumpe für ..." für die Zeit an Minuten die du vorhast, die Pumpe nicht an zu legen. Diese Option setzt eine temp. Basalrate von 0% für den eingestellten Zeitraum. Wenn du die Pumpe früher wieder anlegst, halte wieder die Taste am Bildschirm und wähle "Fortsetzen". Dein IOB wird dadurch genauer für die Berechnungen sein.
* Sicherheitshalber sind die Vorschläge nicht auf die einzelnen BZ Wert gerichtet, sondern anhand des durchschnittlichen Deltas, somit kann es sein, dass du im Falle, wenn du keine BZ Werte bekommen hast, es eine Weile dauern kann bis AndroidAPS wieder anfängt zu loopen.
* Es gibt verschieden Blogs (Englisch), wo es gute Tipps zum loopen gibt:
  * [Warum die Wirkungsdauer von Insulin wichtig ist](http://seemycgm.com/2017/08/09/why-dia-matters/)
  * [Spitzen nach dem essen verringern](https://diyps.org/2016/07/11/picture-this-how-to-do-eating-soon-mode/)
  * [Hormone und Autosens](http://seemycgm.com/2017/06/06/hormones-2/)


### Welche Ausstattung sollte für den Notfall immer vorhanden sein?

### Wie befestige ich das CGM/FGM?

## AndroidAPS Einstellungen

### APS Algorithmus

#### Warum wird "dia:3" in dem "OPENAPS AMA"-Tab angezeigt, obwohl ich in meinem Profil einen anderen angegeben habe?
![AMA 3h](../../images/Screenshot_AMA3h.png) 
In OpenAPS AMA ist das nicht der DIA aus dem Profil, der für das Insulin verwendet wird. Das ist ein anderer Parameter, der fälschlicherweise auf dem DIA aufgebaut wurde. Er bedeutet eher "wann soll die Korrektur abgeschlossen sein" und ist auf 3h begrenzt. Der IOB wird auch nicht mit diesem, sondern dem DIA aus dem Profil berechnet. In  OpenAPS SMB fällt der Parameter dann ganz weg.


### Profil
   
#### Warum wird ein Minimum-DIA (Insulin-end-time) von 5h verwendet anstatt 2-3h?
Das ist gut erklärt in diesem [Artikel (englisch)](/www.diabettech.com/insulin/why-we-are-regularly-wrong-in-the-duration-of-insulin-action-dia-times-we-use-and-why-it-matters/). Don't forget to `ACTIVATE PROFILE` after changing  your DIA.

## weitere Einstellungen 

### Nightscout Einstellungen

### CGM Einstellungen

## Pumpe

### Wohin mit der Pumpe?

### Batterie

* Das Loopen kann die Batterie der Pumpe schneller aufbrauchen. Am besten sollte man die Batterie bei 25% wechseln, weil sich die Pumpe mit schwacher Batterie bei der Kommunikation schwer tut, und es nicht mehr lange dauert bis sie ganz leer ist. Du kannst in Nightscout eine Warnung einrichten, falls du mal vergessen solltest nach dem Stand zu sehen. Tricks um Energie zu sparen:
  * senke die Dauer der Bildschirmbeleuchtung (im Pumpen-Menü einzustellen)
  * senke die Dauer der Bildschirmzeit (im Pumpen-Menü einzustellen)
  * wähle als Benachrichtigung den Ton anstatt des Vibrierens (im Pumpen-Menü einzustellen)
  * benutze die Tasten der Pumpe so selten wie möglich, optimalerweise wird sie nur benutzt beim Auffüllen des Reservoirs. Um vergangene Daten, Batteriestand und Reservoirmenge zu kontrollieren benutze AndroidAPS.
  * Die App AndroidAPS kann öfter vom Android-Betriebssystem des Handies "abgeschossen" werden, um Energie zu sparen oder Speicher freizugeben. Wenn ANdroidAPS dann wieder neu gestartet wird, wird die komplette basalrate und Historie erneut eingelesen, was eine energieintensive lange Bluetooth-Kommunikation erfordert. Um zu prüfen, ob dies häufiger auftritt, kann man im AndroudAPS Menü "Logge App-Start in NS" aktivieren. Dann erscheinen Neustarts in der Blutzucker-Kurve auf dem Hauptbildschirm und in Nigthscout. Sollte die App häufig neu gestartet werden, versuche sie auf der Whiteliste der Prozesse zu setzen, die nicht automatisch beendet werden und im Hintergrund weiterlaufen dürfen. 
  * Reinige die Batterie-Kontakte mit Alkohol
  * Bei der DanaR/RS Pumpe wird während der Startprozedur kurzzeitig mit Hilfe einer hohen Stromstärke versucht, die Schutzfilme auf den Batterie-Kontakten zu entfernen. Manchmal werden diese aber nicht komplett entfernt, dann kann es helfen die Batterie zu entfernen und erneut einzusetzen oder die Batterie außerhalb der Pumpe für den Bruchteil einer Sekunde kurzzuschließen.
   * Einige weitere spezifische Batterie-Tipps zur Accu-Chek Combo findest Du unter [hier](./Accu-Chek-Combo:-Tipps-beim-t%C3%A4glichen-Gebrauch#rund-um-die-pumpen-batterie)

### Wie wechsle ich den Katheter oder des Insulin-Reservoir?

* Der Wechsel der Ampulle kann nicht über AndroidAAPS erfolgen, sondern muss wie bisher **direkt über die Pumpe** durchgefürht werden.
* Dazu durch langes Drucken auf **Closed Loop** auf dem Home-Bildschirm von AndroidAAPS **Pausiere Loop für 1h** auswählen
* Nun Pumpe vom Körper trennen und wie bisher die **Ampulle gemäß der Pumpen-Bedienungsanleitung wechseln**. 
* Anschließend durch langes Drücken auf **Pausiert** wieder **Forsetzen** wählen.

Im Gegensatz zum "klassischen" Vorgehen nutzt AndroidAAPS nicht die "Katheter füllen" Funktion der Pumpe, sondern befüllt den Katheter mit Hilfe eines normalen **Bolus, der nicht in der Historie auftaucht**. Das hat den Vorteil, dass dadurch keine aktuell laufende temporäre Basalrate unterbrochen wird.
* Somit zum Wechseln des Katheters zunächst den alten Katheter entfernen und den neuen anschließen, aber noch nicht setzen.
* Auf dem Tab **AKTIONEN** in AndoidAPS über den Knopf **Vorfüllen/Füllen** die Menge an Insulin einstellen, die zum Befüllen nötig ist und den Füllvorgang starten. Sollte die Menge nicht reichen, den Vorgang ggf. wiederholen. 
* Anschließend den neuen Katheter setzen.

## Hygiene

### Was ist beim Duschen oder Baden zu beachten?
Du kannst die Pumpe zum Duschen oder Baden abstöpseln. Für diese kurze Zeit kommst du normalerweise problemlos ohne sie aus. AAPS solltest du aber Bescheid geben, damit die IOB-Berechnungen stimmen. Dazu drückst du im Home-Screen links oben auf das hellblaue "Open Loop / Closed Loop"- Feld und wählst "Trenne Pumpe für 1 h". Sobald du die Pumpe wieder anschließt, gehst du im selben Feld auf "Fortsetzen".

## Arbeiten

## Sport

## Sex

## Feiern

## Alkoholkonsum

## Schlafen

## Reisen

## Krankenhausaufenthalt

## Termin beim Diabetologen
