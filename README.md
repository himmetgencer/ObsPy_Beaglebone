# ObsPy_Beaglebone
ObsPy on Beaglebone (A Python Framework for Seismology)

AM3358 Debian 10.3 2020-04-06 4GB Bone imajı yüklenir.(Debian 10 Buster)

OBSPY Kurulumu

Method-1(apt)
```sh
echo "deb http://deb.obspy.org buster main" >> /etc/apt/sources.list
wget --quiet -O - https://raw.githubusercontent.com/obspy/obspy/master/misc/debian/public.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install python3-obspy
```

Method-2(PyPi Online)
```sh
sudo apt-get update
sudo apt-get install libatlas-base-dev
optional: sudo pip3 install --upgrade numpy 
sudo pip3 install obspy
```

Method-3(PyPi zip file)[https://pypi.org/project/obspy/#files]
```sh
sudo apt-get update
sudo apt-get install libatlas-base-dev
optional: sudo pip3 install --upgrade numpy 
wget https://files.pythonhosted.org/packages/b8/8c/eef47074a1884c73bc4f2ba7b2961a79fc54952edadeff4b998de86dcb20/obspy-1.2.2.zip
sudo pip3 install obspy-1.2.2.zip
```

RING SERVER Kurulumu
```sh
wget https://github.com/iris-edu/ringserver/archive/v2020.075.tar.gz
tar -xzvf v2020.075.tar.gz
make
```
Example of ring.conf:
```sh
RingSize 100M
RingDirectory /root/ringDir
DataLinkPort 16000
SeedLinkPort 18000
ServerID "TDG_ET_HG"
TransferLogRX 0
MSeedScan /root/ringScanDir StateFile=/root/ringDir/scan.state InitCurrentState=y
```

```sh
./ringserver ring.conf
./slinktool -Q 192.168.2.26:18000
./slinktool -I 192.168.2.26:18000
./slinktool -L 192.168.2.26:18000
```

slinktool kurulumu
```sh
git clone https://github.com/iris-edu/slinktool.git
ezxml make file'da aşağıdaki komutu ekle
	CFLAGS = -std=c99
make
```

Ek Notlar:
Kullanımı zorunlu değildir.

SSH Root İzin
```sh
sudo passwd -d root
nano /etc/ssh/sshd_config
	PermitRootLogin yes
	PermitEmptyPasswords no
	UsePAM no
/etc/init.d/ssh restart	
```
Python 3.8 Kurulumu [https://tecadmin.net/install-python-3-8-ubuntu/]
```sh
sudo apt-get install build-essential checkinstall
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev \
    libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev
	
cd /opt
sudo wget https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz

sudo tar xzf Python-3.8.3.tgz 

cd Python-3.8.3
sudo ./configure --enable-optimizations
sudo make altinstall

python3.8 -V

cd /opt
sudo rm -f Python-3.8.3.tgz
```
Python Remove
```sh
sudo apt list --installed | grep "python"

#lists all versions of python installed in your system

sudo apt remove python3.5 (or the version the above command returned)

#the above Command removes python3.5 from the system.

sudo apt purge python3.5

#the above command removes all the folders and files generated or created by python3.5
```

Installed Packages Query
```sh
sudo dpkg-query -l | less
```

Passwd Remove
```sh
sudo passwd -d root
```
Install specific version
```sh
pip install numpy==1.10.1
```
Reinstall specific version
```sh
sudo python3.7 -m pip install 'numpy>1.0, <1.15' --force-reinstall
```
Add User To Root Group
```sh
sudo usermod -a -G root john
```
Delete User With Root Privileges
```sh
sudo userdel john
```
