# DECA Binaries 

Find the .sof and .svf bitstream binaries under their category (arcades, computer, consoles).

Each binary includes in the filename the date when was made. Older versions go into old folder.

A status list of cores with audio/video/memory options is included [here](DECA_binaries.ods).

![DECA_binaries](DECA_binaries.png)



To flash the bitstreams to the FPGA follow these steps (see detailed instructions in https://github.com/DECAfpga/DECA_board/tree/main/Tutorials/Uploading-Cores):



NOTE about SVF files: all _nodsm.svf files have been edited with [MAX10 SVF Cleaner](https://github.com/opengateware-labs/tools-max10_svf_cleaner) to remove the DSM clear command. This way if you have a bitstream loaded into FPGA flash you won't loose it after flashing any _nodsm.svf file.



## Flash bitstream to FGPA with Quartus

Update with your own PATHs to Quartus and sof filename:

```sh
cd path/to/output_files/
export PATH="/path/to/quartus/bin:$PATH"
quartus_pgm --mode=jtag -o "p;patth/to/core.sof"

```

Example:

```sh
cd deca/output_files/
export PATH="/home/jordi/bin/intelFPGA_lite/17.1/quartus/bin:$PATH"
quartus_pgm --mode=jtag -o "p;gameboy_deca.sof"

```



## Flash bitstream to FGPA with OpenOCD

Execute script as follows updating path/to/altera-usb-blaster2.cfg and  /path/to/file.svf. 

```sh
openocd \
-f path/to/altera-usb-blaster2.cfg \
-d0 \
-c init \
-c "svf -quiet /path/to/file.svf" \
-c shutdown

```

Example:

```sh
openocd -f /home/jordi/Documents/Arduino-DIY/FPGAs/OpenOCD/altera-usb-blaster2.cfg \
-d0 -c init -c "svf -quiet gameboy_deca.svf" -c shutdown

```

