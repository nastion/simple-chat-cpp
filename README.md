
# C++ GUI & Socket Programmierung - Simple Chat

## Die Aufgabenstellung
Erstelle ein einfaches Chatprogramm auf Basis der Abbildungen unter Anwendung
des MVC Design Patterns!

### Grundanforderungen
* GUI's mittels qt-Designer und pyqt5 \[1] erstellen
* Trennung jeweils von View und Controller sowie der Kommunikationsimplementierung
* Sphinx-Dokumentation

#### Client
Die GUI soll ein Eingabefeld f�r Nachrichten und einen Senden-Button implementieren.

Verbindung zum Server Port 5050 wird beim Starten hergestellt - im Fehlerfall
wird eine MessageBox mit dem Fehler angezeigt und das Programm wieder geschlossen.

Bei einem Klick auf "Senden" wird die Nachricht an den Server geschickt und das Textfeld geleert.

In der Grundfunktionalit�t ist ein anonymes Chatten m�glich,
wobei der Chat-Text dann jeweils ganz links beginnt.

Ein zweiter Prozess liest eingehende Nachrichten und f�gt sie in den Chatbereich ein.

Wird die Verbindung geschlossen, schlie�t sich das Programm ohne offene Resourcen zu hinterlassen.
Das Close-Event wird abgefangen und der Socket wird sauber geschlossen.

#### Server
Horcht auf Port 5050 in einem Prozess auf eingehende Verbindungen. Es ist wichtig,
dass accept() in einem eigenen Prozess aufgerufen wird, da sonst die GUI einfriert.

Im Fehlerfall wird eine entsprechende MessageBox angezeigt und das Programm beendet.

Neue Nachrichten an den Server werden an alle Clients verteilt und im eigenen Chat Feld angezeigt.

Wenn der Server geschlossen wird, wird die Verbindung zu allen Clients sauber beendet
und die Clients werden daher automatisch geschlossen.

Achtung: GUI-spezifische Operationen (z.B. Anzeigen einer MessageBox oder Bearbeiten
eines GUI-Elements) d�rfen nur vom GUI-Prozess durchgef�hrt werden -
verwende hierf�r eigene Signals und Slots.

### Erweiterungen
Der User kann den Chatnamen bei Programmaufruf mitgeben.

    python MyChatClient.py ChatName

Ohne Chatname soll in der erweiterten Ausf�hrung jeder anonyme
User einen Chatnamen automatisch erhalten (z.B. "Client 1", "Client 2"),
wobei der chat Text dann jeweils nach dem Doppelpunkt beginnt.
Es wird immer "ChatName: text" gesendet, also "Client 1: Hallo!", "Franz: Servus!".

Neue Clients werden der Client-Liste hinzugef�gt, sobald sie sich verbinden.
F�r jeden neuen Client wird ein neuer Prozess erstellt, welcher auf eingehende Nachrichten wartet.
Wenn ein Client die Verbindung beendet, wird er aus der Client-Liste entfernt.

Der ServerAdmin kann einen Client entfernen indem er ihn in der UserListBox anlickt
und dann den Disconnect Button dr�ckt. Der Server kann also verbundene Clients aus
der Client-Liste entfernen und die Verbindung zu ihnen beenden.

Der Client muss konfiguriert werden, bevor er die Verbindung mit dem Server herstellt:
Parameter sind ChatName, Host, IP.

Im Falle einer langen chat Historie soll die chat List box automatisch ganz
nach unten scrollen damit man bequem mitlesen kann.

Mach dir au�erdem Gedanken �ber Prozesssynchronisation - muss etwas synchronisiert werden?
Wenn ja, was? Halte deine Erkenntnisse hier fest!

GUI skaliert bei einem Resize entsprechend.

### Umgebung und Tests

Als Entwicklungsumgebung wird Visual Studio 2017 verwendet.
<!--
Es wird PyBuilder als Build-Umgebung verwendet. Um eine Liste an Tasks zu erhalten k�nnen folgende Befehle ausgef�hrt werden:

    python setup.py # installs necessary packages
    pyb -t

Um die Umgebung auch f�r PyCharm einzurichten, kann der folgende Task ausgef�hrt werden:

    pyb pycharm_generate

Die Abh�ngigkeiten k�nnen optional auch in einer virtuellen Umgebung geladen werden. Dabei werden alle notwendigen
Pakete in ein eigenes Verzeichnis geladen und die PATH Variable auf dieses Verzeichnis hin angepasst.

Nicht vergessen die definierten GUI-Files mit pyuic5 zu erstellen:
    
    pyuic5 -o src/main/python/clientView.py clientView.ui

Das Beispiel soll entsprechend der mitgelieferten Tests implementiert werden. Folgende Befehle werden bei der Abnahme
ausgef�hrt und bewertet:

    pyb publish run_unit_tests
    pyb sphinx_generate_documentation
-->
## Umsetzung

<!---
Was musste recherchiert werden um die Aufgabe l�sen zu k�nnen?
Welche Erfahrungen wurden gemacht?
Wie ist man zum Ergebnis gekommen?
-->

## Quellen
\[1] Qt manual, Qt Designer manual <http://doc.qt.io/qt-5/>  
\[2] Message Handler Beispiel <http://codingnights.com/coding-fully-tested-python-chat-server-using-sockets-part-1/>

