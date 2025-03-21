# Realizacija hardvera namjenskog računarskog sistema

## Instalacija ***Intel Quartus Prime 20.1 Lite Edition*** skup softverskih alata

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

## Qsys/Platform Designer
U sistemu koji se odnosi na Nios segment trebaju nam sljedece komponente:
1. **PLL**(PLL je predprojektovana komponenta, te samo podesavamo njene parametre da bismo dobili zeljene frekvencije na izlazu)</br>
   - **Nios II** procesor radi na **50MHz**</br>
   - **SDRAM kontroler** radi na **100MHz**</br>
   - **Eksterna SDRAM** radi na **100MHz** (takt koji pogoni eksternu SDRAM mora biti fazno pomjeren(3 758ps) u odnosu na takt koji se dovodi na SDRAM kontroler)</br>
  ![image](https://github.com/user-attachments/assets/613fc694-d69d-4fc8-825f-89e8ffc72b8a) </br>
  
Izlazi PLL-a ce se dovoditi na ulaze drugih komponenata na nacin da:
  - outclk0 od **50MHz** dovodimo na takt ulaz **Nios procesora** i njegovih periferija
  - outclk1 od **100MHz** dovodimo na takt ulaz **SDRAM kontrolera**
  - outclk2 od **100MHz** (fazno pomjeren) dovodimo na takt ulaz **SDRAM**-a (eksterna memorija koja se ne nalazi na chip-u)
