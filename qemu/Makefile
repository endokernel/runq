include ../make.rules

all: image qemu.tar

image:
	cp ../kernel/out/boot/vmlinuz-5.9.8-arch1-cet ./$(ARCH)/vmlinuz-5.9.8-arch1-cet
	mkdir -p ./$(ARCH)/lib
	cp -r ../kernel/out/lib ./$(ARCH)
	cd $(ARCH) && \
	docker build -t $(BUILD_IMAGE) -f ./Dockerfile .

qemu.tar:
	docker run --rm $(BUILD_IMAGE) tar -C $(QEMU_ROOT) -cf - .  > qemu.tar

install: qemu.tar
	rm -rf $(QEMU_ROOT)
	mkdir -p $(QEMU_ROOT)
	tar -C $(QEMU_ROOT) -xf qemu.tar
	chmod 0700 $(QEMU_ROOT)
	chmod 0750 $(RUNQ_ROOT)

clean:
	-rm -f qemu.tar

distclean: clean
	docker rmi -f $(BUILD_IMAGE); echo
