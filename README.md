# PlantVoiceBox

Denne patch skal udgøre en plantes voiceboks i et forsøg på at etablere en dialogisk forbindelse mellem det humane og det non-humane. I patchen anvendes subpatches; [pd ArduinoReceive], [pd DataSmoother], [pd DataScaler]. Disse subpatches ses illustreret og beskrevet gennem denne readme.

![plantvoicebox_v1.1](./media/plantvoicebox_v1.1.png)

https://vimeo.com/manage/videos/576381533

## Externals PD

Derudover anvendes pure data externals der skal downloades for at patchen kan fungere.

comport[v1.1.1]
cyclone[v0.5-5]

for at downloade externals til PD

![findExternal](./media/findExternal.png)

![External](./media/External.png)

## Arduino Connection

I min udviklings proces hard jeg anvendt en LDR for at simulere det analoge input fra EMG sensoren. Arduino aflæser det analoge signal via A0. Arduino sketchen uploades til boardet.

![ArduinoCode](./media/ArduinoCode.png)

For at forbinde Arduino til Pure Data anvendes objektet [comport 0 9600] ved at trykke på comport knappen, vil en liste af arduino com-porte blive vist i pd's konsol. Ud for hver com-port vises et index-nr. 

![AvailableComports](./media/AvailableComports.png)

Her er min comport nr. 21 /dev/tty.usbmodem1421. For at åbne comporten i puredata anvendes et "message"-objekt [open 21] for at åbne comport index 21. For at ændre Arduino kode skal data-stream stoppes ved at trykke på "message"-objektet [close].

![ArduinoRecieve](./media/ArduinoRecieve.png)

fra [pd ArduinoReceive]-objektet outputtes alle analoge outlets fra Arduino.

## DataSmoothing

for at gøre det analoge input mere anvendeligt køres signalet gennem en DataSmoother. Således gøres det meget omskiftlige signal mere roligt.

![DataSmoother](./media/DataSmoother.png)

## Data Scaling

afhængigt af hvilken plante, sensor, etc. kan det analoge input variere og derfor anvendes en DataScaler for bedre at kunne tilpasse signalets værdier.

![DataScaler](./media/DataScaler.png)

## Data Latch Envelope Trigger

For at gøre det lydlige udtryk mere dialogisk anvendes noget old-school computer memory logik som en måde at aktivere en envelope der medvirker til at det lydlige udtryk går fra en drone til en mere rytmisk udtryk.

![DataLatchEnvelopeTrigger](./media/DataLatchEnvelopeTrigger.png)

## Future Work

- I det fremtidige arbejde med patchen ønskes at gøre det lydlige udtryk mere spændende ved at tilføje elementer fra [formant syntese](https://en.wikipedia.org/wiki/Formant) der vil resultere i en klang der kan minde mere om en menneske stemmes, hvilket jeg tænker vil være hensigtsmæssig i forhold til [GrowingCoDesigns](https://www.growingcodesign.com/) anvendelse af critical anthromorphization og non-human kvaliteter. Da klangen ved formant syntese netop befinder sig i spændet mellem mennesket stemme og det ikke menneskelige.
- implementering med RaspberryPi og det øvrige hardware/software system.

## Sources

- https://www.youtube.com/watch?v=eVW0FD9g_Sk
- https://www.growingcodesign.com/
- https://www.instagram.com/growingcodesign/
- https://mikemorenoaudio.wordpress.com/2016/09/06/first-blog-post-formant-filters-with-pd-pt-1/