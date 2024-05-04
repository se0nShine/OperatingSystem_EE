# OperatingSystem_EE

# XV6 install guide

1. Ubuntu 18.04.4 LTS를 설치
2. 개발환경 설정을 위한 다음 명령어들 터미널에서 실행

```bash
sudo apt-get upgrade
sudo apt-get install build-essential
sudo apt-get install gcc-multilib
sudo apt-get install git
Sudo apt-get install qemu
```

3. xv6 설치를 위해 다음 명령어들 실행

```bash
cd
git clone https://github.com/se0nShine/OperatingSystem_EE/xv6_ssu_init.tar.gz.git
tar xvzf xv6_ssu_init.tar.gz
cd xv6_ssu_init
make qemu-nox
```

4. Trouble shooting

make qemu-nox 안될경우 kernel.ld를 수정을 해야함 

파일내 BYTE(0) 부분이 총 두개가 있는데 이를 주석처리한다.

수정 전 code

```bash
.stab : {
		PROVIDE(__STAB_BEGIN__ = .);
		*(.stab);
		PROVIDE(__STAB_END__ = .);
		BYTE(0)		/* Force the linker to allocate space
				   for this section */
	}

	.stabstr : {
		PROVIDE(__STABSTR_BEGIN__ = .);
		*(.stabstr);
		PROVIDE(__STABSTR_END__ = .);
		BYTE(0)		/* Force the linker to allocate space
				   for this section */
	}
```

수정 후 code

```bash
.stab : {
		PROVIDE(__STAB_BEGIN__ = .);
		*(.stab);
		PROVIDE(__STAB_END__ = .);
		/*BYTE(0)		Force the linker to allocate space
				   for this section */
	}

	.stabstr : {
		PROVIDE(__STABSTR_BEGIN__ = .);
		*(.stabstr);
		PROVIDE(__STABSTR_END__ = .);
		/*BYTE(0)	  Force the linker to allocate space
				   for this section */
	}
```
