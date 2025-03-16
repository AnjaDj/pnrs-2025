# Projektovanje namjenskih računarskih struktura
<p align="left">
  <img src="/image/ne.png" alt="Description" width="750" height="400"/>
</p>

## O projektu
Radi se na hibridnom SoC sa predprojektovanim procesorskim dijelom ***HPS*** i konfigurabilnim ***FPGA*** dijelom.</br>
- Potrebno je realizovati ***Soft Processor Nios II*** i osnovne periferije koji se instanciraju na osnovu ***FPGA*** strukture.
- Potrebno je flash-ovati Linux OS na microSD za kontrolu rada ***HPS***-a.
- Potrebno je ostvariti komunikaciju izmedju ***HPS*** i ***Nios II*** procesora.
- Potrebno je omoguciti pristup periferijama koje su instancirane na ***FPGA*** strani, sa strane ***HPS*** dijela.
- Krajnji cilj jeste kreirati multiprocesorski sistem na bazi vise ***Soft Nios II processor-a*** koji dijele zajednicke resurse i periferije.
  

## Hardver
Hardver koristen u sklopu kursa je ***DE1-SoC*** development board [user-manual](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=167&No=836&PartNo=4#contents) </br>
<p align="left">
  <img src="/image/de1soc.png" alt="Alt text" width="550" height="450"/>
</p>

***DE1-SoC*** je razvojna ploča sa hibridnim ***CycloneV SoC*** koji uključuje:</br>
<img src="/image/cpu.png" alt="icon" width="30" height="30"/> ***HPS*** - Hard Processor System predprojektovani Dual-core ARM procesor</br>
<img src="/image/fpga" alt="icon" width="30" height="30"/> ***FPGA*** - na osnovu kog ćemo kreirati ***Soft processor*** i nekih dodatnih periferiija</br>
<p align="left">
  <img src="/image/cyclonev.png" alt="Alt text" width="550" height="450"/>
</p>

## Softver
Softver koristen u sklopu kursa:
-  <img src="/image/quartus" alt="icon" width="25"/> Quartus Prime Lite 16.01 (uz alat *Sopc Builder/Qsys/Platform Designer*)
-  <img src="/image/niosiiprocessor.png" alt="icon" width="25"/> Nios II Software Build Tools (Za razvoj aplikacija za Nios II Soft Procesor koji se realizuje u okviru FPGA dijela)
- SoC Embedded Design Suite (za razvoj Linux aplikacija koje se izvrsavaju na HPS procesoru)

## Cilj 🎯

Cilj kursa jeste dobiti odgovore na sledeća pitanja:</br>
   ❓Kako kreirati ***Soft Processor*** koji se instancira na osnovu ***FPGA*** strukture?</br>
   ❓Kako ***Soft Processor*** i ***HPS*** mogu međusobno komunicirati i dijeliti periferije?</br>
   ❓Kako napisati Bare-metal aplikaciju za ***Nios II Soft processor***?</br>
   ❓Kako flash-ovati Linux OS na SD karticu koji će konfigurisati i inicijaliyovati ***HPS***?</br>
   ❓Kako napisati Linux aplikaciju za ***HPS***?</br>
   ❓Kako iz ***HPS***-a mozemo pristupiti periferijama koje su instancirane na ***FPGA*** strani?</br>
   ❓Kako instancirati vise ***Nios II*** procesora kako bismo napravili multiprocesorski sistem?</br>
   ❓Kako multiprocesorski sistem moze da dijeli zajednicke resurse?</br>
