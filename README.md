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
