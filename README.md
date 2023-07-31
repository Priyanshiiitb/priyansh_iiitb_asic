# priyansh_iiitb_asic
## Day1 [Installation]
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





