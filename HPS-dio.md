# Realizacija dijela sistema sa HPS procesorom i periferijama na HPS i FPGA dijelu chipa
Cilj je da napravimo skup periferija sa HPS strane kojima HPS moze direktno pristupiti (LED i taster), te da omogucimo da 
HPS ima pristup periferijama sa FPGA strane (7s displeji i tasteri).

### Qsys - HPS procesor
Komunikacija izmedju **HPS** i **FPGA** dijela ce se svoditi na jednosmjernu komunikaciju u smislu da ce HPS procesor koristiti
periferije sa FPGA dijela chipa.</br>
 - ✖️ Iskljucujemo opciju *FPGA-to-HPS interface* jer necemo sa FPGA strane pristupati HPS periferijama.</br>
 - ✖️ Nemamo Hi-performance periferije sa velikim protokom podataka od HPS-a ka FPGA dijelu, iskljucicemo i opciju *HPS-to-FPGA interface*.</br>
 - ✔️ Koristimo samo ***Lightweight HPS-to-FPGA interface*** koji nam omogucava da sa HPS strane pristupimo memorijski mapiranim periferima na FPGA dijelu.

![image](https://github.com/user-attachments/assets/dc798d97-d827-4ffe-ae07-9df3c3f8c041)

**PinMux podesavanje**:

- Zelimo da koristimo **Ethernet** jer ce nam biti neophodan za **debugovanje**. **Ethernet interfejs** je vezan na kontroler **EMAC1**.
- **SD MMC controler** da bismo mogli bootati sistem sa kartice. Koristi se 4bit-ni prenos podataka.
- **UART kontroler**
- **HPS-KEY / HPS-LED** su vezani na G21/A24 sto znaci da zelimo **G21/A24** vezati na funkciju **HPS_GPIO54/HPS_GPIO53**.

![image](https://github.com/user-attachments/assets/92a4c1ce-1f51-4d36-ad1e-51ad72274fdb)
![image](https://github.com/user-attachments/assets/d8f164cc-eb60-4254-825e-0ea5b868ee9b)

Interupt za Ethernet je vezan za pin **C19** i treba ga vezati za funkciju **HPS_GPIO35**</br>
![image](https://github.com/user-attachments/assets/d2b4b59d-a4aa-4838-993d-e00e74ae91fd)

**SDRAM podesavanje**:
SDRAM koji se nalazi na HPSu je povezan na DDR3, za njegovo podesavanje koristicemo **[presets](presets/de1-soc-hps-ddr.qprs)**.


### Povezivanje

**hps_io** je interfejs za povezivanje sa periferijama samog HPS-a exportovanih na pinove HPS dijela.
