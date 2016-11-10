QEMU = qemu-2.7.0
QEMUPKG = $(QEMU).tar.bz2
QEMUURL = http://wiki.qemu-project.org/download/$(QEMUPKG)
QEMUDIR = $(QEMU)
QEMUACH = x86_64-softmmu
QEMUOUT = $(QEMUDIR)/$(QEMUACH)
QEMUBIN = $(QEMUOUT)/qemu-system-x86_64
QEMUIMG = $(QEMUDIR)/qemu-img
QEMUOPT = -enable-kvm -m 8192 -smp 4 -serial stdio
QEMUVGL = -display gtk,gl=on -vga virtio -soundhw ac97 
QEMUVM1 = -redir tcp:10022::22 -drive file=$(IMG1PATH),if=virtio
QEMUVM2 = -redir tcp:10122::22 -drive file=$(IMG2PATH),if=virtio
QEMUCDR = -cdrom $(ISOPATH) -boot order=cd

ISOFILE = Fedora-Workstation-Live-x86_64-24-1.2.iso
ISOPATH = ../ISO/$(ISOFILE)

IMG1FILE = fc.qcow2
IMG1PATH = ../IMG/$(IMG1FILE)
IMG2FILE = fc2.qcow2
IMG2PATH = ../IMG/$(IMG2FILE)

all:
	@echo "make [qemu|vminstall|vmstart]"

qemu: preinstall
	@[ -f $(QEMUPKG) ] && echo "$(QEMUPKG) exist" || wget $(QEMUURL)
	@[ -d $(QEMUDIR) ] && echo "$(QEMUDIR) exist" || tar -xf $(QEMUPKG)
	cd $(QEMUDIR) && \
	./configure \
		--enable-debug \
		--audio-drv-list=alsa,oss \
		--enable-virglrenderer \
		--enable-opengl \
		--enable-gtk \
		--target-list=$(QEMUACH) && \
	make

# libasound2-dev => --audio-drv-list=alsa,oss => -soundhw ac97
preinstall:
	apt-get -y install \
	libzip-dev \
	libgtk-3-dev \
	libgbm-dev \
	libgl1-mesa-dev \
	libasound2-dev

VIRGLDIR = virglrenderer
virgl:
	@[ -d $(VIRGLDIR) ] || git clone https://anongit.freedesktop.org/git/virglrenderer.git
	cd $(VIRGLDIR) && \
	./autogen.sh && make && make install

vminstall:
	[ -f $(IMG1PATH) ] && echo "$(IMG1PATH) exist" || $(QEMUIMG) create -f qcow2 $(IMG1PATH) 20G
	$(QEMUBIN) $(QEMUOPT) $(QEMUVM1) $(QEMUCDR)

vm1start:
	$(QEMUBIN) $(QEMUOPT) $(QEMUVM1) $(QEMUVGL)

vm2start:
	$(QEMUBIN) $(QEMUOPT) $(QEMUVM2) $(QEMUVGL)
