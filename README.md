# priyansh_iiitb_asic
## Table of Contents
- [Week - 1](#week---1)
    * [Day - 1 : Software Installation](#day---1--software-installation)
- [Week - 2](#week---2)
    * [Day - 1 : Introduction to Verilog RTL Design and Synthesis](#day---1--introduction-to-verilog-rtl-design-and-synthesis)
	* [Day - 2 : Timing libs, Hierarchical vs Flat Synthesis and Efficient flop coding styles](#day---2--timing-libs-hierarchical-vs-flat-synthesis-and-efficient-flop-coding-styles)
	* [Day - 3 : Combinational and Sequential Optimisations](#day---3--combinational-and-sequential-optimisations)
	* [Day - 4 : Gate Level Simulation (GLS), Blocking Vs Non-blocking assignment and Synthesis-Simulation Mismatch](#day---4--gate-level-simulation-gls-blocking-vs-non-blocking-assignment-and-synthesis-simulation-mismatch)
	* [Day - 5 : If, case, for and for generate](#day---5--if-case-for-and-for-generate)

  
## Week - 1 
## Day - 1 : Software Installation


## YOSYS
Steps involve in Ubuntu
```
git clone https://github.com/YosysHQ/yosys.git
cd yosys-master 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make 
sudo make install
```
Just image for confirmation

![Screenshot from 2023-07-31 10-01-30](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/e8c1e5b8-70cc-4ece-b397-bb656cf40baa)


## Verilog
## steps
```
sudo apt-get install iverilog
```
Just image for confirmation
![Screenshot from 2023-07-31 10-01-57](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/8c624e10-1b35-46b0-8fd4-9a9939897254)

## Gtkwave
## steps
```
sudo apt-get -y install gtkwave
```
Just image for confirmation
![Screenshot from 2023-07-31 10-02-17](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/33ed1cb2-3fd6-47fd-b471-28b0506cf52e)

## Magic
## Steps
```
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
```
Here screenshot for confirmation
![Screenshot from 2023-07-31 13-46-47](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/49385d0b-1080-48d1-997a-5a17eddf8d8a)

## Ngspice
## Steps
```
tar -zxvf ngspice-40.tar.gz
cd ngspice-40
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
```
![Screenshot from 2023-07-31 21-07-56](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/45a75b32-bd3d-4553-9c8f-9d9df3684e3e)

## OpenSTA
## Steps
```
sudo apt-get install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
![Screenshot from 2023-07-31 21-09-46](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/735098b0-2a9c-42c4-98b6-5a4dcacce761)
## Openlane
## steps
```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git

sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io

sudo docker run hello-world

sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 

# After reboot
docker run hello-world
```

![Screenshot from 2023-07-31 21-49-43](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/7b044e62-4e2f-4862-9d19-95525c28d17a)
## Week - 2
## Day - 1 : Introduction to Verilog RTL Design and Synthesis

### Here is the code for 2:1MUX and its test bench:
```
module good_mux (input i0 , input i1 , input sel , output reg y); 
	always @ (*)
	begin
		if(sel)
		y <= i1;
		else 
		y <= i0;
	end
endmodule


`timescale 1ns / 1ps
module tb_good_mux;
// Inputs
reg i0,i1,sel;
// Outputs
wire y;
  		// Instantiate the Unit Under Test (UUT), name based instantiation
	good_mux uut (.sel(sel),.i0(i0),.i1(i1),.y(y));
	//good_mux uut (sel,i0,i1,y);  //order based instantiation
initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
end
always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
end module
```
### Following command used

![Screenshot from 2023-08-12 09-47-38](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/7d9d7f0b-2e10-4ada-be4a-d5fa8237d4ac)
### Below is the gtkwave plot:

![Screenshot from 2023-08-12 09-48-13](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/e862f54a-7f44-4ca2-b077-a28b9c038c7f)

## Yosys Synthesizer
###  flow of Yosys Synthesize
![166094901-27c70c0d-8ef2-4a34-a4b2-7307af492698](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/ae73847d-1a55-48a1-9f95-b58911faded8)

### Below are the commands to perform above synthesis.

RTL Design - read_verilog |
.lib - read_liberty  |
netlist file- write_verilog
### How to enter yosys
![Screenshot from 2023-08-12 09-53-21](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/4251baf0-dbc2-4ca6-a86a-02a110909c18)

```
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
yosys> read_verilog good_mux.v 
yosys> synth -top good_mux 
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
yosys> show
```

![Screenshot from 2023-08-12 09-53-37](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/cdd3c7c5-db62-49b6-843f-0081361d2a5c)
![Screenshot from 2023-08-12 09-55-32](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/de028f2c-5382-44fd-b154-004b26941604)
### Below is the screenshot of synthesized design:
![Screenshot from 2023-08-12 09-56-24](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/0d80633b-8116-49ba-b3e8-f50202737e0d)
### Netlist code:
```
yosys> write_verilog good_mux_netlist.v 
yosys> !vim good_mux_netlist.v 


```
![Screenshot from 2023-08-12 10-02-12](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/44689966-ea6d-466c-b8d7-5f98799f4ed5)
### Simplified netlist code: This code consisits of additional switch. To further simplify, we use below command
```
yosys> write_verilog -noattr good_mux_netlist.v
yosys> !vim good_mux_netlist.v

```
![Screenshot from 2023-08-12 10-13-49](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/f2edef02-ed58-46d5-b40d-4d98f810cfa4)

## Day - 2 : Timing libs, Hierarchical vs Flat Synthesis and Efficient flop coding styles
### LAB- Introduction to  .lib

**With in the lib file, the gates are delared as follows to meet the variations due to process, temperatures and voltages.**

![Screenshot from 2023-08-12 14-43-04](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/3f4457d1-6c26-4b8a-8c41-fbaba2685692)
### below image displays the power consumption comparision and size of transistor in increasing order but delay will be opposite of this.
![Screenshot from 2023-08-12 15-01-17](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/f2563d66-df72-4fc7-b75f-8880ab2eb5aa)

### LAB- Hierarchical synthesis and flat synthesis
```

yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog 
read_verilog multiple_modules.v 
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show multiple_modules
write_verilog multiple_modules_hier.v
```
![Screenshot from 2023-08-12 15-15-45](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/1ffff5b2-57e5-4c26-9b11-93db5c6a5389)
![netlist_hier](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/3dd03282-8d3b-4bcf-b6f6-6f5d3b0e7c6b)

```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
 read_verilog 
 read_verilog multiple_modules.v 
 synth -top multiple_modules
 abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
 flatten
 show
 write_verilog multiple_modules_flat.v
```
![flat_des](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/30837c2d-7d31-437b-94d3-f51a250bb35a)
![netlist_flat](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/def217b5-a002-421f-b3ef-b97e268086b5)

### Steps to synthesis submodule :
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog 
read_verilog multiple_modules.v 
synth -top sub_module
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show

```
![submodule_synth](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/34220aa7-10f2-4e2f-944c-3da76371b933)
### Various Flop coding styles and optimization
### 1. D flip-flop with Synchronous reset
A D flip-flop with synchronous reset  combines the functionality of a D flip-flop with the ability to reset its state synchronously. This means that the flip-flop's stored value can be reset to 0 or low state based on a clock signal and a reset input, ensuring that the reset operation occurs when the clock signal transits.
The verilog code, simulation and synthesis results are shown below:
```
module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
	if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```



### 2. D flip-flop with Asynchronous reset

![Screenshot from 2023-08-12 16-41-48](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/691ddf23-ad7d-4f82-8b54-8a30d2e23129)

A D flip-flop with asynchronous reset combines the functionality of a D flip-flop with the ability to reset its state asynchronously. This means that the flip-flop's stored value can be reset to 0 or low state regardless of the clock signal's state.
The verilog code, simulation and synthesis results are shown below:
```
module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```



### 3. D flip-flop with Asynchronous set
A D flip-flop with asynchronous set combines the functionality of a D flip-flop with the ability to set its state asynchronously. This means that the flip-flop's stored value can be set to 1 or high state regardless of the clock signal's state.
The verilog code, simulation and synthesis results are shown below:

```
module dff_async_set ( input clk ,  input async_set , input d , output reg q );
always @ (posedge clk , posedge async_set)
begin
	if(async_set)
		q <= 1'b1;
	else	
		q <= d;
end
endmodule
```
![Screenshot from 2023-08-12 16-44-07](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/6c7f6f66-94cf-4cf6-b7bd-55a4d024e569)




### 4. D flip-flop with Asynchronous and Synchronous reset
A D flip-flop with both asynchronous and synchronous reset that combines the features of a D flip-flop with the ability to reset its state using either an asynchronous reset input or a synchronous reset input. This provides flexibility in resetting the flip-flop's state under different conditions.

The verilog code, simulation and synthesis results are shown below:

```
module dff_asyncres_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```

### Screenshots
### asynchronous rest

![Screenshot from 2023-08-12 16-41-48](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/691ddf23-ad7d-4f82-8b54-8a30d2e23129)

### asynchronous set


![Screenshot from 2023-08-12 16-44-07](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/6c7f6f66-94cf-4cf6-b7bd-55a4d024e569)

## Day - 3 : Combinational and Sequential Optimisations
### Combinational logic optimization with examples



Techniques for optimization:

* Constant propagation which is Direct optimizxation technique 
* Boolean logic optimization using K-map or Quine McKluskey
### Example 1  
```
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```
![Screenshot from 2023-08-12 21-03-57](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/3e86c1f7-bea3-493d-b61c-d4804895023c)
### Example 2
```
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```
![Screenshot from 2023-08-12 21-17-41](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/70a90f9c-e309-4c5a-a40c-3b557590e4af)

### Example 3
```
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```
![Screenshot from 2023-08-12 21-21-17](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/9e3a0260-eb72-4a09-93e7-c21f390e25cd)
### Example 4
```
module opt_check4 (input a , input b , input c , output y);
	assign y = a?(b?(a & c ):c):(!c);
endmodule
```
![Screenshot from 2023-08-12 21-24-53](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/27fe70f7-51ec-45dd-93ee-11f2f4c997c9)
### Sequential Logic Optimization with examples
### Example-1
Here flop will be inferred as the output is not constant.
```
module dff_const1(input clk, input reset, output reg q);
	always @(posedge clk, posedge reset)
	begin
		if(reset)
			q <= 1'b0;
		else
			q <= 1'b1;
	end
endmodule
```
![Screenshot from 2023-08-13 18-09-21](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/659883b5-0e3f-4c33-b9e8-4d5b0c42676b)
![Screenshot from 2023-08-13 18-09-21](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/ce3c0138-fd8a-4373-9714-217ad95ce067)
### Example-2
Here flop will not be inferred as the output is always high.
```
module dff_const2(input clk, input reset, output reg q);
	always @(posedge clk, posedge reset)
	begin
		if(reset)
			q <= 1'b1;
		else
			q <= 1'b1;
	end
endmodule
```
![Screenshot from 2023-08-13 18-10-18](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/56ba9e3d-3514-400c-93ac-1501a0b7a418)
![Screenshot from 2023-08-13 18-17-20](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/2de66206-4725-4c63-8bf4-b2a1a15eb666)
### Example 3
```
	module dff_const3(input clk, input reset, output reg q);
	reg q1;

	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b1;
			q1 <= 1'b0;
		end
		else
		begin
			q1 <= 1'b1;
			q <= q1;
		end
	end
	endmodule
```
![Screenshot from 2023-08-13 18-46-49](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/3d1ddf92-98e1-48f8-973e-cd0a72e44e56)
![Screenshot from 2023-08-13 18-19-15](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/560ecbce-df8e-45f2-a909-ec4aabba5df2)
### Example 4
```
	module dff_const4(input clk, input reset, output reg q);
	reg q1;

	always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b1;
			q1 <= 1'b1;
		end
	else
		begin
			q1 <= 1'b1;
			q <= q1;
		end
	end
	endmodule
```
![Screenshot from 2023-08-13 18-56-00](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/730767a3-61ff-4f6a-ad0b-caa9d1e0d6c8)
![Screenshot from 2023-08-13 19-22-34](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/9ea60edf-ebb2-440e-bd4b-b25e2da2817c)

### Example 5
```
	module dff_const5(input clk, input reset, output reg q);
	reg q1;
	always @(posedge clk, posedge reset)
		begin
			if(reset)
			begin
				q <= 1'b0;
				q1 <= 1'b0;
			end
		else
			begin
				q1 <= 1'b1;
				q <= q1;
			end
		end
	endmodule
```
![Screenshot from 2023-08-13 18-57-13](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/21278706-a26e-4deb-82cf-a4dfa7782af2)

![Screenshot from 2023-08-13 20-47-20](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/28715f8e-b642-4ad7-8889-9d179357aa26)
### Sequential optimisation of unused outputs
```
module counter_opt (input clk , input reset , output q);
	reg [2:0] count;
	assign q = {count[2:0]==3'b100};
	always @(posedge clk ,posedge reset)
	begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
	end
endmodule
```
![Screenshot from 2023-08-13 20-52-57](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/818ba8ac-5810-4d0a-b2e2-dd94620fea6a)



## Day - 4 : Gate Level Simulation (GLS), Blocking Vs Non-blocking assignment and Synthesis-Simulation Mismatch


### GLS, Synthesis-Simulation mismatch and Blocking, Non-blocking statements


### Synthesis Simulation Mismatch

There are three main reasons for Synthesis Simulation Mismatch:<br />
* Missing sensitivity list in always block
* Blocking vs Non-Blocking Assignments
* Non standard Verilog coding

 **Missing sensitivity list in always block:**<br />

If the consider - Example-2, we can see the only **sel** is mentioned in the sensitivity list. During the simulation, the waveforms will resemble a latched output but the simulation of netlist will not infer this as the synthesizer will only look at the statements with in the procedural block and not the sensitivity list.

As the synthesizer doen't look for sensitivity list and it looks only for the statements in procedural block, it infers correct  circuit  and if we simulate the netlist code, there will be a synthesis simulation mismatch.

To avoid the synthesis and simulation mismatch. It is very important to check the behaviour of the circuit first and then match it with the expected output seen in simulation and make sure there are no synthesis and simulation mismatches. This is why we use GLS.

**Blocking vs Non-Blocking Assignments**:

Blocking statements execute the statemetns in the order they are written inside the always block. Non-Blocking statements execute all the RHS and once always block is entered, the values are assigned to LHS. This will give mismatch as sometimes, improper use of blocking statements can create latches. Get to see at Example4 

 ### Lab- GLS Synth Sim Mismatch 

 **Example-1** There is no mismatch in this example as the netlist simulation and rtl simulation waveform are similar only
```
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
endmodule
```
![Screenshot from 2023-08-14 10-03-41](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/73ec9b93-79c3-4ff5-94ae-b8f7097a614f)
![Screenshot from 2023-08-14 10-08-43](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/f5db1258-5b46-484c-9e7c-2d4ea62c61fb)
### Example 2
```
module bad_mux (input i0 , input i1 , input sel , output reg y);
	always @ (sel)
	begin
		if(sel)
			y <= i1;
		else 
			y <= i0;
	end
endmodule
```
![Screenshot from 2023-08-14 10-39-10](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/52438c99-d626-488a-bf86-c1db74acd041)
### Net Simulation
![Screenshot from 2023-08-14 10-51-50](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/1d1634a2-ae49-4ce3-8715-49c2439fbc66)
### MISMATCH
Here second pic shows the netlist simulation which corrects the bad_mux design which was only changing waveform when sel was triggered while for a mux to work properly it should be sensitivity to all the input signals

### Example 3
```
module good_mux (input i0 , input i1 , input sel , output reg y);
	always @ (*)
	begin
		if(sel)
			y <= i1;
		else 
			y <= i0;
	end
endmodule
```




### Lab- Synthesis simulation mismatch blocking statement

### Example 4
```
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
	begin
	d = x & c;
	x = a | b;
end
endmodule
```
![Screenshot from 2023-08-14 11-11-26](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/dec5d57b-b74d-4b7f-9aed-43e04a7b3d5e)
### Netlist
![Screenshot from 2023-08-14 11-19-07](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/303ebd5e-88ea-4f69-9489-2a8f378454c4)

Here second pic show the netlist simulation which shows the proper working of the dut while the first pic shows the improper working of dut as we have used blocking statement here which causes synthesis simulation mismatch which is sorted out by GLS while providing netlist simulation

## Day - 5 : If, case, for and for generate
### Lab- Incomplete IF
### Example 1
This incomplete if construct forms a connection between i0 and output y i.e, D-latch with input as i1 and i0 will be the enable for it.
```
module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
end
endmodule
```
![Screenshot from 2023-08-14 22-10-07](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/dffab73a-1036-42a3-ab01-89fc9daa787f)
![Screenshot from 2023-08-14 22-13-21](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/8508b504-4042-42f8-824b-a577a16f3be7)

### Example 2

The below code is equivalent to two 2:1 mux with i0 and i2 as select lines with i1 and i3 as inputs respectively. Here as well, the output is connected back to input in the form of a latch with an enable input of OR of i0 and i2.
```
module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
	always @ (*)
	begin
		if(i0)
			y <= i1;
		else if (i2)
			y <= i3;
	end
endmodule

```
![Screenshot from 2023-08-14 22-33-18](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/cb6c8a99-ec3e-496e-a35f-7cb3187df6d4)
![Screenshot from 2023-08-14 22-35-26](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/fbf20119-8743-4461-b18c-99ba46e1ed50)

### Lab- incomplete overlapping Case
### Example-1
Thie is an example of incomplete case where other two combinations 10 and 11 were not included. This is infer a latch for the multiplexer and connect i2 and i3 with the output.
```
module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
	always @ (*)
	begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
	endcase
	end
endmodule
```
![Screenshot from 2023-08-14 22-40-31](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/382e1a5f-1e82-4ea9-9596-23fa5ce1da3e)
![Screenshot from 2023-08-14 22-43-18](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/1974059e-7eb6-495a-a90a-642cdcc5ba30)

### Example-2- Complete case
```
module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
		default : y = i2;
	endcase
end
endmodule
```
![Screenshot from 2023-08-15 09-16-17](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/632601d3-909e-46e1-a1b8-ee0ae9366d49)
![Screenshot from 2023-08-15 09-18-10](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/97f3f993-ec0e-4b2e-bc95-f0b9edbbb0b5)
### example-3
In the below example, y is present in all the case statements and it had particular outut for all cases. There no latch is inferred in case of y. When it comes to x, it is not assigned for the input 01, therefore a latch is inferred here.
```
module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
always @ (*)
begin
	case(sel)
		2'b00 : begin
			y = i0;
			x = i2;
			end
		2'b01 : y = i1;
		default : begin
	         	  x = i1;
			  y = i2;
		 	 end
	endcase
end
endmodule
```
![Screenshot from 2023-08-15 09-24-25](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/a77087c6-b78d-4290-9873-a9b24d288451)

### For Loop and For Generate



**For Loop**<br />
- For look is used in always block
- It is used for excecuting expressions alone

**Generate For loop**<br />
- Generate for loop is used for instantaing hardware
- It should be used only outside always block

For loop can be used to generate larger circuits like 256:1 multiplexer or 1-256 demultiplexer where the coding style of smaller mux is not feesible and can have human errors since we would need to include huge number of combinations.

FOR Generate can be used to instantiate any number of sub modules with in a top module. For example, if we need a 32 bit ripple carry adder, instead of instantiating 32 full adders, we can write a generate for loop and connect the full adders appropriately.


### Lab- For and For Generate
### Example-1- Mux using generate
Here for loop is used to design a 4:1 mux. This can also be written using case or if else block, however, for a large size mux, only for loop model is feasible.
```
module mux_generate (input i0 , input i1, input i2 , input i3 , input [1:0] sel  , output reg y);
	wire [3:0] i_int;
	assign i_int = {i3,i2,i1,i0};
	integer k;
always @ (*)
	begin
	for(k = 0; k < 4; k=k+1) begin
		if(k == sel)
		y = i_int[k];
		end
	end
endmodule
```
![Screenshot from 2023-08-15 09-39-50](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/ada36d49-2cca-4039-a650-966adf32a09e)
![Screenshot from 2023-08-15 09-50-28](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/05c672d9-5bcf-479c-9a7d-884e1136e11e)
### Example-2-Demux using Case
```
module demux_case (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
reg [7:0]y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @ (*)
begin
y_int = 8'b0;
case(sel)
	3'b000 : y_int[0] = i;
	3'b001 : y_int[1] = i;
	3'b010 : y_int[2] = i;
	3'b011 : y_int[3] = i;
	3'b100 : y_int[4] = i;
	3'b101 : y_int[5] = i;
	3'b110 : y_int[6] = i;
	3'b111 : y_int[7] = i;
endcase
end
end module
```
![Screenshot from 2023-08-15 09-53-47](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/6450d7d6-a8bf-403a-a7f9-27ab7ed37c47)
![Screenshot from 2023-08-15 09-55-52](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/5c816f5b-b8d6-48ea-9bac-45185304c7c7)



### Example-3-Demux using Generate

The code in above example is big and also there is a chance of human error wile writing the code. However, using for loop as shown below, this drawback can be elimiated to a great extent.
```
module demux_generate (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
reg [7:0]y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @ (*)
begin
	y_int = 8'b0;
	for(k = 0; k < 8; k++) begin
		if(k == sel)
		y_int[k] = i;
	end
end
endmodule

```
![Screenshot from 2023-08-15 10-02-54](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/aaaa0883-6e26-46a0-9545-7148ec978dbf)
![Screenshot from 2023-08-15 10-05-14](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/d7143c83-b91f-4752-8341-7d3e45ea3585)
### Netlist simulation
![Screenshot from 2023-08-15 10-07-05](https://github.com/Priyanshiiitb/priyansh_iiitb_asic/assets/140998626/dbe0176d-a07c-435d-8eb4-cb2f68278f4d)






## Acknowledgement
- Kunal Ghosh, VSD Corp. Pvt. Ltd.
- Skywater Foundry
- Alwin Shaju,colleague,IIITB 
- Kanish R,Colleague,IIIT B
- Nanditha Rao, Professor, IIITB 
- Madhav Rao, Professor, IIITB
- Manikandan,Professor,IIITB
  
## Reference 

- https://github.com/YosysHQ/yosys.git
- https://github.com/The-OpenROAD-Project/OpenSTA.git
- https://github.com/kunalg123
- https://www.vsdiat.com
  

  
