# priyansh_iiitb_asic
##  Contents
- [Week - 1](#week---1)
    * [Day - 1 : Software Installation](#day---1--software-installation)
- [Week - 2](#week---2)
    * [Day - 1 : Introduction to Verilog RTL Design and Synthesis](#day---1--introduction-to-verilog-rtl-design-and-synthesis)
	* [Day - 2 : Timing libs, Hierarchical vs Flat Synthesis and Efficient flop coding styles](#day---2--timing-libs-hierarchical-vs-flat-synthesis-and-efficient-flop-coding-styles)
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


