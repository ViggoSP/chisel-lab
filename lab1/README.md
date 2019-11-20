# Lab Session 1

## Hello World in Chisel

The lab session will show you a Hello World example (a blinking LED) in Chisel.
We will explore the tools needed for the Chisel based design flow.

After the lab you will have a good overview of the tools used to
edit and compile a hardware design coded in Chisel.
You will be able to synthesize this design and configure the FPGA board.

We assume that you have downloaded the complete lab material from GitHub
and it is placed in folder ```chisel-lab```.

### Background Reading

 * This lab is loosely based on Chapter 1 of
*[Digital Design with Chisel](https://github.com/schoeberl/chisel-book/wiki)*

### Exploring and Compiling the Hello World Component

With IntelliJ import the lab1 project as follows:

 * Start IntelliJ
 * Click *Import Project*
 * Navigate to ```.../chisel-lab/lab1``` and select the file ```build.sbt```, press *Open*
 * Press OK on the next dialog box

This importing from the project may take some time at the first import, as Scala and Chisel files need to be downloaded. Wait until it is finished.

> If you have an IntelliJ project already open, you can create a new project with:
> *File - New - Project from Existing Sources...*

Then navigate to the Chisel component ```Hello``` by following in the Project navigator along: *lab1 - src - main - scala - Hello*. Open ```Hello``` with a double click.

This is a complete Chisel component including generation of a slower logical time
to drive a blinking LED at 1 Hz from the 100 MHz clock from the Basys3 board.
Do not get intimidated by those about 20 lines of code, you will soon understand the
details. Today's lab topic is to get the tool flow working down to a configured FPGA.

Open the sbt shell at the bottom of IntelliJ window. This will take some time
at the first time (displaying initializing). When it is ready type
```
run
```
to compile and run your project.

In the *Run* window you should see something like:
```
[info] Running HelloMain 
Hello World, I will now generate the Verilog files!
[info] [0.001] Elaborating design...
[info] [2.205] Done elaborating.
Total FIRRTL Compile Time: 916.6 ms
[success] Total time: 22 s, completed Jul 22, 2019 11:09:25 AM
```
This is the output of the Chisel compiler und runtime. To see that the program
runs we provide a friendly greeting message, starting with the famous "Hallo World".
If your design contains errors, you will see error messages in this window.

Running the Chisel program generates a Verilog file (```Hello.v```) that we
use for synthesizing our design for an FPGA. The content of this file is not
important, but for curiosity you might open it right from within IntelliJ.

**CLI Alternative:**

If you do not like to use an IDE, you can work at the command line
(shell, terminal). Use a program editor of you choice and open ```Hello.scala```
found at ```.../lab1/src/main/scala/Hello.scala```.
You compile and run the *Hello World* in Chisel from the command line with a simple:

```bash
sbt run
```

Future lab projects may contain a ```Makefile``` that you can execute with ```make```.

**End CLI Alternative**

### Synthesizing and Configuring the FPGA with Vivado.

We use the Xilinx tool
[Vivado](https://www.xilinx.com/products/design-tools/vivado/vivado-webpack.html)
to synthesize our design and configure the Basys3 board.

The process is described in detail in the document
*A digital circuit design flow guide  using VHDL and Xilinx Vivado
targeting a Digilent BASYS 3 FPGA board* from last semester.
Please use that document (available in DTU Inside).
The following list is only a brief summary.

#### Vivado Project Creation

 * Open Vivado
 * Click *Create Project*
 * Click *Next*
 * Pick a name and a location and click *Next*
   * You might place your project under ```chisel-lab/lab1```
 * Click *Next* to accept an *RTL Project*
 * In the next dialog box click *Add Files* and navigate to ```Hello.v``` and add it
 * At the *Add Constraints* dialog box clock *Add Files* and select
   ```Basis3Hello.xdc``` and press *OK*.
   * For the following labs you will need to edit the constraints file derived
     from the Basys3 Master constraints file.
 * Click *Next*
 * In the *Default Part* dialog box select *Boards* and the *Basys3*, press *Next*
 * Press *Finish* to create the project

#### Synthesize and Configure the FPGA Board

We are just a few clicks away from running our great *Hello World* design in
the Basys3 board.

 * Connect your Basis3 board with the USB cable to your laptop
 * Click on *Generate Bitstream* at the bottom of the *Project Manager* to
   start synthesis, implementation, and bitstream generation
   * This process may take some time (minutes)
 * Configure your FPGA with *Program Device* under *Open Hardware Manager*
   * Open hardware manager after bitfile generation
   * Open target, Auto Connect
   * Program device

You should now see an LED blinking at 1 Hz.

**Congratulation! You have build your first digital design in Chisel**

After this lengthy setup, the next run of the design flow should be smooth.
Try to change the ```CNT_MAX``` constant to a slightly smaller value
(e.g., 50000000 instead of 100000000) to change the blinking frequency.
Run the Chisel code in IntelliJ again and synthesize and configure again
with Vivado. The LED should now blink at a different frequency.
Faster or slower? At what frequency?
