# Realizacija hardvera namjenskog računarskog sistema

Cilj jeste napraviti sistem koji ce se sastojati od
  - Nios segmenta koji ce imati neke komponente(programabilni ulaz/izlaz) povezane na Nios procesor
  - HPS segment
Za potrebe opisa hardvera sistema koga zelimo projektovati, bice nam potreban ***Quartus Prime*** softverski alat, te je preduslov za dalji rad upravo instalacija pomenutom softverskog alata.</br>

## 📥	Instalacija ***Intel Quartus Prime 20.1 Lite Edition*** skup softverskih alata

Sa zvanične Intel [stranice](https://www.intel.com/content/www/us/en/software-kit/661019/intel-quartus-prime-lite-edition-design-software-version-20-1-for-windows.html) biramo sledeće opcije:
![image](https://github.com/user-attachments/assets/e6c24e49-2b53-4a4e-9c9d-163d8fa6120c) </br>

U ***Downloads*** sekciji ispod, biramo ***Individual Files***, te download-ujemo: 
- **ModelSim-Intel® FPGA Edition**
- **Intel® Quartus® Prime (includes Nios® II EDS)**
- **Intel® Cyclone® V Device Support**

Pokrećemo Quartus Lite Setup, uz selekciju sledećih komponenata
<p align="left">
  <img src="/image/select.png" alt="Alt text" width="250" height="200"/>
</p>

## Kreiranje ***Quartus*** projekta
Nakon sto je proces instalacije zavrsen, pokrecemo ***Quartus Prime*** softverski alat, te kreiramo novi projekat</br> <i>File->New Project Wizard</i>. Potrebno je voditi racuna o tome da se izaberu sljedece opcije u sklopu **Family, Device & Board Settings** prozora:
  - Family: Cyclone V (E/GX/GT/SX/SE/ST)
  - Device: Cyclone V SE Mainstream
  - Board : **5CSEMA5F31C6**

Kao **top level** entitet koristimo entitet definisan u ***[VHDL fajlu](hdl/de1_soc_top.vhd)***. Top level entitet treba da opise strukturu citave ploce.</br>
Top level entitet definise ulazne i izlazne pinove, ali ih je neophodno pridruziti hardverskim stvarnim pinovima. To mozemo raditi rucno, ali i preko **tcl** skripte.
 ***[Tcl skriptu](tcl/pin_assignment_de1_soc.tcl)*** koja ce uraditi pin assignment, pokrecemo preko Tools->Tcl scripts...->Run</br>
<img src="https://github.com/user-attachments/assets/97745647-4b9b-47ea-9832-420d799da17d" width="600"> </br></br>


## Opis hardverskog sistema
Za potrebe opisa hardvera sistema koga zelimo projektovati, koristicemo alat ***Tools/Qsys(Platform Designer)***.</br>
Od komponenata koje se odnose na Nios segment ce nam trebati sledece komponente:

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
