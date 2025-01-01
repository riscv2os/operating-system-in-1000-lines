(env) cccimac@cccimacdeiMac operating-system-in-1000-lines % ./run.sh
+ QEMU=qemu-system-riscv32
+ CC=/opt/homebrew/opt/llvm/bin/clang
+ OBJCOPY=/opt/homebrew/opt/llvm/bin/llvm-objcopy
+ CFLAGS='-std=c11 -O2 -g3 -Wall -Wextra --target=riscv32 -ffreestanding -nostdlib'
+ /opt/homebrew/opt/llvm/bin/clang -std=c11 -O2 -g3 -Wall -Wextra --target=riscv32 -ffreestanding -nostdlib -Wl,-Tuser.ld -Wl,-Map=shell.map -o shell.elf shell.c user.c common.c
+ /opt/homebrew/opt/llvm/bin/llvm-objcopy --set-section-flags .bss=alloc,contents -O binary shell.elf shell.bin
+ /opt/homebrew/opt/llvm/bin/llvm-objcopy -Ibinary -Oelf32-littleriscv shell.bin shell.bin.o
+ /opt/homebrew/opt/llvm/bin/clang -std=c11 -O2 -g3 -Wall -Wextra --target=riscv32 -ffreestanding -nostdlib -Wl,-Tkernel.ld -Wl,-Map=kernel.map -o kernel.elf kernel.c common.c shell.bin.o
+ cd disk
+ tar cf ../disk.tar --format=ustar hello.txt meow.txt
+ qemu-system-riscv32 -machine virt -bios default -nographic -serial mon:stdio --no-reboot -d unimp,guest_errors,int,cpu_reset -D qemu.log -drive id=drive0,file=disk.tar,format=raw,if=none -device virtio-blk-device,drive=drive0,bus=virtio-mmio-bus.0 -kernel kernel.elf

OpenSBI v1.5.1
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name             : riscv-virtio,qemu
Platform Features         : medeleg
Platform HART Count       : 1
Platform IPI Device       : aclint-mswi
Platform Timer Device     : aclint-mtimer @ 10000000Hz
Platform Console Device   : uart8250
Platform HSM Device       : ---
Platform PMU Device       : ---
Platform Reboot Device    : syscon-reboot
Platform Shutdown Device  : syscon-poweroff
Platform Suspend Device   : ---
Platform CPPC Device      : ---
Firmware Base             : 0x80000000
Firmware Size             : 319 KB
Firmware RW Offset        : 0x40000
Firmware RW Size          : 63 KB
Firmware Heap Offset      : 0x47000
Firmware Heap Size        : 35 KB (total), 2 KB (reserved), 10 KB (used), 22 KB (free)
Firmware Scratch Size     : 4096 B (total), 244 B (used), 3852 B (free)
Runtime SBI Version       : 2.0

Domain0 Name              : root
Domain0 Boot HART         : 0
Domain0 HARTs             : 0*
Domain0 Region00          : 0x00100000-0x00100fff M: (I,R,W) S/U: (R,W)
Domain0 Region01          : 0x10000000-0x10000fff M: (I,R,W) S/U: (R,W)
Domain0 Region02          : 0x02000000-0x0200ffff M: (I,R,W) S/U: ()
Domain0 Region03          : 0x80040000-0x8004ffff M: (R,W) S/U: ()
Domain0 Region04          : 0x80000000-0x8003ffff M: (R,X) S/U: ()
Domain0 Region05          : 0x0c400000-0x0c5fffff M: (I,R,W) S/U: (R,W)
Domain0 Region06          : 0x0c000000-0x0c3fffff M: (I,R,W) S/U: (R,W)
Domain0 Region07          : 0x00000000-0xffffffff M: () S/U: (R,W,X)
Domain0 Next Address      : 0x80200000
Domain0 Next Arg1         : 0x87e00000
Domain0 Next Mode         : S-mode
Domain0 SysReset          : yes
Domain0 SysSuspend        : yes

Boot HART ID              : 0
Boot HART Domain          : root
Boot HART Priv Version    : v1.12
Boot HART Base ISA        : rv32imafdch
Boot HART ISA Extensions  : sstc,zicntr,zihpm,zicboz,zicbom,sdtrig,svadu
Boot HART PMP Count       : 16
Boot HART PMP Granularity : 2 bits
Boot HART PMP Address Bits: 32
Boot HART MHPM Info       : 16 (0x0007fff8)
Boot HART Debug Triggers  : 2 triggers
Boot HART MIDELEG         : 0x00001666
Boot HART MEDELEG         : 0x00f0b509


virtio-blk: capacity is 3072 bytes
file: hello.txt, size=83
file: meow.txt, size=6
> ls
unknown command: ls
> 