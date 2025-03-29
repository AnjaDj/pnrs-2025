# Realizacija dijela sistema sa HPS procesorom i periferijama na HPS i FPGA dijelu chipa
Cilj je da napravimo skup periferija sa HPS strane kojima HPS moze direktno pristupiti (LED i taster), te da omogucimo da 
HPS ima pristup periferijama sa FPGA strane (7s displeji i tasteri).

### Qsys - HPS procesor
Komunikacija izmedju **HPS** i **FPGA** dijela ce se svoditi na jednosmjernu komunikaciju u smislu da ce HPS procesor koristiti
periferije sa FPGA dijela chipa.</br>
 - ✖️ Iskljucujemo opciju *FPGA-to-HPS interface* jer necemo sa FPGA strane pristupati HPS periferijama.</br>
 - ✖️ Nemamo Hi-performance periferije sa velikim protokom podataka od HPS-a ka FPGA dijelu, iskljucicemo i opciju *HPS-to-FPGA interface*.</br>
 - ✔️ Koristimo samo ***Lightweight HPS-to-FPGA interface*** koji nam omogucava da sa HPS strane pristupimo memorijski mapiranim periferima na FPGA dijelu.
