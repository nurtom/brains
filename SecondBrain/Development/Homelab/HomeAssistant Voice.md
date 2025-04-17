## Hardware
- 2025/04/15 Ordered 2 x Home Assistant Voice Preview Edition via seeedstudio.com for 141,56 USD
- Einrichtung mit Home Assistant Cloud Trial (bis 18.05.2025)
- Einrichtung via Home Assistant Mobile App

# Notes
## Lokale Sprachverarbeitung
### Benötigte Integrationen
#### Wyoming Protocol
- Kommunikation zwischen den Services, wird als Integration im HA aktiviert
#### Whisper
- Speech to text
- Dienst kann irgendwo separat laufen, muss in der Integration konfiguriert werden
#### Piper
- Text to speech
- Dienst kann irgendwo separat laufen, muss in der Integration konfiguriert werden


## Beispiel Voice Commands

okay nabu ...

```text
küche pause
küche weiter
küche stop

nächster titel küche
pausiere küche
küche fortsetzen
küche lautstärke auf 40%
stoppe küche

wie ist die temperatur im wohnzimmer?

wie ist der solarertrag?


```
