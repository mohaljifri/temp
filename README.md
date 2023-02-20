the following steps on debian 11 x86_64
# temp
su
mkdir /synology
cd /synology

wget https://sourceforge.net/projects/dsgpl/files/Tool%20Chain/DSM%206.2.4%20Tool%20Chains/Intel%20x86%20Linux%203.10.105%20%28Cedarview%29/cedarview-gcc493_glibc220_linaro_x86_64-GPL.txz/download

wget https://sourceforge.net/projects/dsgpl/files/Synology%20NAS%20GPL%20Source/25426branch/cedarview-source/linux-3.10.x.txz/download

cp cedarview-gcc493_glibc220_linaro_x86_64-GPL.txz /usr/local/

cd /usr/local/
tar -xJf cedarview-gcc493_glibc220_linaro_x86_64-GPL.txz
tar -xJf cedarview-gcc493_glibc220_linaro_x86_64-GPL.txz
tar -xJf linux-3.10.x.txz


tar -xJf cedarview-gcc493_glibc220_linaro_x86_64-GPL.txz

x86_64-pc-linux-gnu
linux-3.10.x

export CFLAGS="-I/usr/local/x86_64-pc-linux-gnu/include" &&
export LDFLAGS="-I/usr/local/x86_64-pc-linux-gnu/lib" &&
export RANLIB=/usr/local/x86_64-pc-linux-gnu/bin/x86_64-pc-linux-gnu-ranlib &&
export LD=/usr/local/x86_64-pc-linux-gnu/bin/x86_64-pc-linux-gnu-ld &&
export CC=/usr/local/x86_64-pc-linux-gnu/bin/x86_64-pc-linux-gnu-gcc &&
export LD_LIBRARY_PATH=/usr/local/x86_64-pc-linux-gnu/lib &&
export ARCH=x86_64 &&
export CROSS_COMPILE=/usr/local/x86_64-pc-linux-gnu/bin/x86_64-pc-linux-gnu- &&
export KSRC=/synology/linux-3.10.x/

cd /synology/linux-3.10.x/
cp synoconfigs/cedarview .config
 make oldconfig
 sudo apt-get install libncurses5-dev libncursesw5-dev
 make menuconfig

make dep
nano /arch/x86/tools/relocs.c
[
change line 695 https://stackoverflow.com/questions/64130032/trouble-compiling-kernel
-Elf_Addr per_cpu_load_addr;
to
+static Elf_Addr per_cpu_load_addr;
]
make modules

cd /synology
git clone https://github.com/kelebek333/rtl8188fu.git
cd rtl8188fu
make KSRC=/synology/linux-3.10.x/
