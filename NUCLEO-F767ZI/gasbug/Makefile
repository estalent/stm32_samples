
ARMGNU = arm-none-eabi

XCPUx = -mcpu=cortex-m0
XCPU = -mcpu=cortex-m7

AOPS = --warn --fatal-warnings $(XCPU)
COPS = -Wall -O2 -nostdlib -nostartfiles -ffreestanding $(XCPU)

all : notmain.bin

clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list

#---------------------------------

flash.o : flash.s
	$(ARMGNU)-as $(AOPS) flash.s -o flash.o

test.o : test.s
	$(ARMGNU)-as $(AOPS) test.s -o test.o

notmain.o : notmain.c
	$(ARMGNU)-gcc $(COPS) -mthumb -c notmain.c -o notmain.o

notmain.bin : flash.ld flash.o test.o notmain.o
	$(ARMGNU)-ld -o notmain.elf -T flash.ld flash.o test.o notmain.o
	$(ARMGNU)-objdump -D notmain.elf > notmain.list
	$(ARMGNU)-objcopy notmain.elf notmain.bin -O binary

