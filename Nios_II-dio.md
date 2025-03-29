# Realizacija hardvera namjenskog računarskog sistema

Cilj jeste napraviti sistem koji ce se sastojati od
  - ***Nios segmenta*** - Nios II procesor sa SDRAM na koji su povezane periferije (programabilni I/O) 
  - ***HPS segment*** koji se sastoji od HPS procesora\

Za potrebe opisa hardvera sistema koga zelimo projektovati, bice nam potreban ***Quartus Prime*** softverski alat, te je preduslov za dalji rad upravo instalacija pomenutom softverskog alata.</br>

[Uputstvo](Instalacija-Quartus-Prime-i-kreiranje-projekta.md) za instalaciju Intel Quartus Prime alata i kreiranje Quartus projekta se nalazi u sklopu repozitorijuma.


## Opis hardverskog sistema
Za potrebe opisa hardvera sistema koga zelimo projektovati, koristicemo alat ***Tools/Qsys(Platform Designer)***.</br>
Od komponenata koje se odnose na **Nios segment** ce nam trebati sledece komponente:
  - Nios II procesor
  - SDRAM kontroler (za komunikaciju sa eksternom SDRAM)
  - periferije povezane na Nios II procesor (LEDs i switch-evi)
  - System ID (kozistencija izmedju softvera pisanog za jedan hardverski sistem i hardverskog sistema na kome ce se izvrsavati taj softver)
  - JTAG UART za pristup konzoli
  - PLL (ne rade sve komponente na istoj frekvenciji)

### Qsys/Platform Designer - PLL konfiguracija
**PLL** je predprojektovana komponenta, te samo podesavamo njene parametre da bismo dobili zeljene frekvencije na njenom izlazu</br>
   - **Nios II** procesor radi na **50MHz**</br>
   - **SDRAM kontroler** radi na **100MHz**</br>
   - **Eksterna SDRAM** radi na **100MHz** (takt koji pogoni eksternu SDRAM mora biti fazno pomjeren(3 758ps) u odnosu na takt koji se dovodi na SDRAM kontroler)</br>
<img src="https://github.com/user-attachments/assets/613fc694-d69d-4fc8-825f-89e8ffc72b8a" width="500"> </br>
  
Izlazi PLL-a ce se dovoditi na ulaze drugih komponenata na nacin da:
  - outclk0 od **50MHz** dovodimo na takt ulaz **Nios procesora** i njegovih periferija
  - outclk1 od **100MHz** dovodimo na takt ulaz **SDRAM kontrolera**
  - outclk2 od **100MHz** (fazno pomjeren) dovodimo na takt ulaz **SDRAM**-a (eksterna memorija koja se ne nalazi na chip-u)

Prva 2 takt signala se dovode na interne komponente u sklopu chip-a, dok se treci takt signal dovodi na eksternu SDRAM koja se nalazi na razvojnoj ploci ali van chip-a. Zbog toga 
je potrebno ***export***-ovati outclk2 tako da bude vidljiv na izlazu</br>
<img src="https://github.com/user-attachments/assets/a64fec32-6afc-4898-9555-23332c479645"  height="150"></br>

<img src="https://github.com/user-attachments/assets/40fbfe7c-895a-45fd-ab52-25ea3564c2ad"  width="350">


### Qsys/Platform Designer - SDRAM kontroler
SDRAM kontroler komunicira sa eksternom SDRAM. Prilikom konfigurisanja SDRAM kontrolera koristili smo ***[presets](presets/sdram-controller.qprs)*** fajl odnosno fajl sa vec predefinisanim parametarima SDRAM komponente. 
<img src="https://github.com/user-attachments/assets/b2c4a301-df4d-44ec-8ccc-213bcf4613fc"></br>
<img src="https://github.com/user-attachments/assets/7e8f42de-d3de-4931-af60-42431a38c2c9"></br>


### Qsys/Platform Designer - Nios II procesor
<img src="https://github.com/user-attachments/assets/632fe881-c461-43f4-8be7-f97055eb45d5">


### Qsys/Platform Designer - System ID peripheral
Kompajler uporedjuje **System ID** hardverskog sistema sa **System ID** sistema za koji je namijenjena aplikacija. Ukoliko postoji razlika, tada ce se prijaviti greska i program nece moci biti izvrsavan na hardveru. Ovo je bitno da bi se osigurala kozistencija izmedju softvera pisanog za jedan hardverski sistem i hardverskog sistema na kome ce se izvrsavati taj softver.
Nema potrebe za rucnim podesavanjem parametara System ID Peripheral komponente jer ce prilikom generisanja sitema, **System ID** biti generisan automatski.
<img src="https://github.com/user-attachments/assets/8770b79c-48f0-4d00-b0a9-7ffc3e96008e">


### Qsys/Platform Designer - JTAG UART
Za konzolni pristup Nios II procesoru. UART koji je preko JTAG-a vezan sa razvojnim okruzenjem za pisanje aplikacija za Nios II procesor. Preko **Avalon magistrale** vezujemo se na JTAG koji je povezan na programer sistema.
<img src="https://github.com/user-attachments/assets/c210ed02-86d1-4379-937d-427fb62097fa">


### Qsys/Platform Designer - Periferije PIO interfejs
Ukljucujemo PIO za povezivanje sa digitalnim IO podsistemom.
Jedan PIO ce biti za LED, imamo 10 LED. Drugi ce biti za switch-eve, imamo 10 switch-eva.</br>
<img src="https://github.com/user-attachments/assets/21cc3582-6f47-415c-bcd6-8e858399fb64">
<img src="https://github.com/user-attachments/assets/2be69a09-7318-4688-bf60-f9ed60ef1aad"> <br>

⚠️ Warning: Kada imamo povezivanje sa spoljnim komponentama (LED, switch, SDRAM), moramo imati ***export-ovan Conduit*** interfejs!


### Povezivanje Nios II komponenata

**Nios procesor** je sada povezan sa **takt sistemom** i **memorijom**. Procesor moze da kontrolise 2 **periferije** LEDs i switches. Imamo mogucnost debagovanja preko **JTAG UART**-a. Takodje je obezbijedjena konzistentnost softvera i hardvera preko **System ID**.
![image](https://github.com/user-attachments/assets/98990412-04d8-47bf-b5db-fd93a06994f3)
![image](https://github.com/user-attachments/assets/7687e83d-b8c5-4386-a66f-8d85434959d9)
