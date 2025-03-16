# Projektovanje namjenskih računarskih struktura

## Hardver
Hardver koristen u sklopu kursa je DE1-SoC development board [user-manual](https://www.terasic.com.tw/cgi-bin/page/archive.pl?Language=English&CategoryNo=167&No=836&PartNo=4#contents)
!["DE1-SoC"](https://github.com/user-attachments/assets/5927317d-beab-4fe1-ac15-7042d3cba534)

DE1-SoC je razvojna ploča sa hibridnim CycloneV SoC koji uključuje:
1. ***HPS*** (Hard Processor System) - predprojektovani procesor
2. ***FPGA*** - na osnovu kog ćemo kreirati ***Soft processor*** i nekih dodatnih periferiija</br>
!["CycloneV"](https://github.com/user-attachments/assets/f005a11a-60c9-4dd2-bd7e-5b7202263476)

## Cilj 🎯

Cilj kursa jeste dobiti odgovore na sledeća pitanja:
1. Kako kreirati ***Soft Processor*** koji se instancira na osnovu ***FPGA*** strukture?
2. Kako ***Soft Processor*** i ***HPS*** mogu međusobno komunicirati i dijeliti periferije?
3. Kako napisati Bare-metal aplikaciju za ***Nios II Soft processor***?
4. Kako flash-ovati Linux OS na SD karticu koji će konfigurisati i inicijaliyovati ***HPS***?
5. Kako napisati Linux aplikaciju za ***HPS***?
6. Kako iz ***HPS***-a mozemo pristupiti periferijama koje su instancirane na ***FPGA*** strani?
7. Kako instancirati vise ***Nios II*** procesora kako bismo napravili multiprocesorski sistem?
8. Kako multiprocesorski sistem moze da dijeli zajednicke resurse?
