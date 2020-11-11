1.  들어가기에 앞서
    1.  WSL
        1.  Windows Subsystem for Linux 
        2.  윈도우10에서 리눅스 실행 파일(ELF)를 실행하기 위한 compatibility layer다.
            1.  ELF
                1.  Executable and Linkable Format
                2.  리눅스, 유닉스의 File format이다.(윈도우는 PE format)
        3.  윈도우에서 GNU/Linux 환경의 파일, 명령어들을 실행시킬 수 있게 된다.
            1.  기존의 cmd가 아닌 lunux kernal의 terminal을 이용할 수 있다.
            2.  하지만 docker도 돌아가긴 하지만 여러가지 설정을 해줘야하는 등,, 조금 어거지스러운 점이 있었다.
    2.  WSL2
        1.  Hyper-v를 사용하여 vm환경에서 linux를 돌릴 수 있게 되었다. 하지만, 기존의 vm환경과는 다르다고 한다.
        2.  기존의 VM환경보다 부팅속도가 빠르며 리소스를 적게 사용하며 windows와 linux간의 호환성을 제공한다. 또한, VM을 구성하거나 관리할 필요가 없다.
    3.  WSL vs WSL2
        1.  WSL은 linux가 돌아가고 메모리 관리를 윈도우 프로세서가 가져와서 한다.
        2.  WSL2는 Hyper-v위에 윈도우와 linux를 돌리는 것이기 때문에, VM과 같은 환경이라고 보면 된다. 따라서, 메모리 관리도 linux에서 직접 하게 된다.
    4.  Windows에서 Linux에 네트워킹
        1.  WSL환경과 달리 WSL2는 가상머신 환경이므로 ip를 알아야 한다.
            1.  WSL로 실행했을 경우 windows host ip와 ubuntu ip가 같다.
        2. ``ip addr``명령어를 실행하여 ``eth0``의 ``ip``값을 확인해야 한다.
    5. Linux에서 Windows에 네트워킹
       1. 호스트 머신의 ``ip``주소를 사용해야 한다.
       2. > cat /etc/resolv.conf
2. 설치
   1. Terminal 설치
      1. 윈도우 스토어에서 ``terminal``을 검색하여 설치한다.
   2. WSL2 활성화
      1. > dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   3. 재부팅
   4. [클릭하여 WSL2 설치](https://docs.microsoft.com/ko-kr/windows/wsl/wsl2-kernel)
   5. Virtual Machine 기능 사용
      1. > dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   6. 윈도우 스토어에서 ``ubuntu``를 설치한다.
      1. **Quick Create Virtual Machine으로 설치가 안되는 경우 수동으로 재시작하여 준다.**
         1. windows security
         2. App & Browser control
         3. Exploit protection
         4. Program settings
         5. ``C:\Windows\System32\vmcompute.exe``를 edit하여 ``Control flow guard``에서 ``Override system settings``를 체크 해제시켜준다.
         6. 터미널에서 명령어 입력
            1. > net start vmcompute
   7. WSL2를 기본 버전으로 설정
      1. > wsl --set-default-version 2
   8. ``ubuntu``를 실행하여 계정설정을 한다.
3. 설치 후 
   1. ``ubuntu``를 실행하여 정상 작동하는지 확인
   2. 작동이 안될 경우 다음을 확인
      1. ``ctrl``+``shift``+``esc``을 눌러 ``서비스``에서 ``LxssManager``를 재시작한다.
      2. 또는 재부팅
   3. 관리자 권한으로 ``terminal``을 연다.
   4. ``wsl2``로 ``ubuntu``가 실행되고 있는지 확인
      1. > wsl -l -v
      2. ``ubuntu`` 버전이 ``1``이라면 ``2``로 변경해줘야 한다.
         1. > wsl --set-version Ubuntu 2
4. 도커 실행
   1. 도커 ``설정``의 ``Resource``에서 ``WSL INTEGRATION``부분의 ``Ubuntu``를 활성화해주면 ``ubuntu``에서도 명령어를 통해 ``docker``를 실행시킬 수 있다.
5. IP체크
   1. ``ip addr`` ``command``를 통해 ``ip``를 확인해보면 ``window``의 ``ip``와 ``Gateway``가 다른 것을 확인할 수 있다. 이는 ``vm``의 환경이기 때문이며, 진짜 ``vm``의 환경과는 또 차이가 있다.


       
  