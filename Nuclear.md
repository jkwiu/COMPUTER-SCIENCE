1. msf
    1.  포트 스캔
        1.  ``service postgresql start``
        2.  ``msfdb init``
            1.  최초 한 번만
        3.  ``msfconsole``
        4.  ``db_nmap -sT -sV -O ip``
        5.  ``db_services``
    2.  brute-force-attack
        1.  준비
            1.  Crunch
                1.  무차별 대입 공격에 필요한 비밀번호 항목을 생성할 수 있다.
                2.  ``crunch 1 4 -f /usr/share/crunch/charset.lst numeric -o /root/passwords.txt``
            2.  ``cat >> /root/passwords.txt`` ``postgres``
            3.  ``cat >> /root/users.txt`` ``administrator`` ``sa`` ``root`` ``postgres``
        2.  시작
            1.  FTP Service
                1.  ``use auxiliary/scanner/ftp/ftp_login``
                2.  ``set rhosts ip``
                3.  ``set user_file /root/users.txt``
                4.  ``set pass_file /root/passwords.txt``
                5.  ``set stop_on_success true``
                6.  ``set threads 256``
                7.  ``run``
            2.  SMB Service
                1.  ``use auxiliary/scanner/smb/smb_login``
                2.  ``set rhosts ip``
                3.  ``set user_file /root/users.txt``
                4.  ``set pass_file /root/passwords.txt``
                5.  ``set stop_on_success true``
                6.  ``set threads 256``
                7.  ``run``
            3.  MS-SQL
                1.  ``use auxiliary/scanner/mssql/mssql_login``
                2.  ``set rhosts ip``
                3.  ``set rport 1433``
                4.  ``set user_file /root/users.txt``
                5.  ``set pass_file /root/passwords.txt``
                6.  ``set stop_on_success true``
                7.  ``set threads 256``
                8.  ``run``
            4.  MYSQL
                1.  3306
            5.  Postgresql
                1.  5432
2.  컴퓨터 메모리
    1.  RAM(Random Access Memeory)
        1.  저장된 어떤 데이터 조각이든 언제든지 읽을 수 있기 때문에 임의 접근이라고 함
    2.  Endian
        1.  Little Endian
        2.  Bing Endian
    3.  메모리 단편화
        1.  Segmentation의 개념
            1.  각 프로세스는 자신이 사용하는 메모리 영역에 접근하길 원한다.
            2.  이 때 한 프로세스가 다른 프로세스의 데이터를 덮어쓰는 일은 원하지 않는다.
            3.  그렇기 때문에 작은 조각으로 단편화되어 프로세스에 넘겨지게 된다.
            4.  레지스터는 이 단편화 조각을 저장하고 추적한다.
    4.  메모리 속 프로그램
        1.  아래와 같은 순서로 이어져 있으며, 낮은 주소부터 높은 주소까지다.
            1.  .text 섹션
                1.  함수가 저장된다.
                2.  해당 테스크를 실행하는 데 필요한 지시사항을 담고 있다.
                3.  읽기 전용이며 쓰려고 하면 단편화 오류를 일으킨다.
                4.  프로세스가 처음 적재된 런타임 시 크기가 고정된다.
            2.  .data 섹션
                1.  전역변수와 정적변수를 저장한다.
                2.  이 섹션의 크기는 런타임 시 고정된다.
            3.  .bss 섹션(Below Stack Section)
                1.  초기화 되지 않은 전역변수 및 정적변수를 저장한다.
            4.  Heap 섹션
                1.  동적으로 할당된 변수를 저장할 때 사용하며 낮은 메모리에서 높은 메모리로 할당된다.
                2.  maloc()과 free()함수로 제어한다.
            5.  Stack 섹션
                1.  함수 호출을 재귀적으로 추적하며 대부분의 시스템에서 높은 주소의 메모리에서 낮은 주소의 메모리로 할당한다.
                2.  이러한 특성 때문에 버퍼 오퍼플로 오류가 발생한다.
            6.  환경/인수 섹션
                1.  런타임 시 프로세스가 요구하는 시스템 수준 변수의 복사본을 저장
                2.  이 섹션이 쓰기 가능하기 때문에 형식 문자와 버퍼 오버플로 취약점을 통해 악용할 수 있다.
        2.  버퍼
            1.  프로세스에 의해 처리되기까지 데이터를 보관해두는 저장소
            2.  프로세스 메모리의 .data, .bss섹션에 메모리를 할당한다.
            3.  버퍼는 한 번 할당되면 고정된 길이를 가진다.
        3.  메모리 속 문자열
            1.  메모리에 저장된 연속적인 문자배열
        4.  포인터
            1.  다른 메모리 조각의 주소를 저장한 특수한 메모리 조각dㅇb
3.  셸코드(Shellcode)
    1.  업무를 수행하는 독립 바이너리 코드
    2.  커널과 통신하는 법
        1.  하드웨어 인터럽트
            1.  키보드의 비동기 신호
        2.  하드웨어 트랩
            1.  ``0으로 나눌 수 없음``과 같은 에러
        3.  소프트웨어 트랩
            1.  실행을 위해 예정된 프로세스에 대한 요청
            2.  윤리적 해커에게 가장 유용한 방법
    3.  커널은 사용자로부터 기초적인 시스템 수준 함수를 추출하고 시스템 호출을 통한 인터페이스를 제공한다.
4.  시스템 호출
    1.  ``execve``시스템 호출
        1.  ``$man 2 execve``
    2.  어셈블리 수준에서는 다음 레지스터가 시스템 호출시 로딩된다.
        1.  eax
            1.  시스템 호출의 16진수 값을 로딩하는 데 사용
        2.  ebx
            1.  첫 번째 파라미터
        3.  ecx
            1.  두 번째 파라미터
        4.  edx
            1.  세 번째 파라미터
        5.  esi
            1.  네 번째 파라미터
        6.  edi
            1.  다섯 번째 파라미터
            2.  다섯 개가 넘으면 파라미터 배열을 메모리에 저장하고 이 주소를 ``ebx``에 저장해야 된다.
    3.  동작 순서
        1.  레지스터가 로딩되면 ``int 0x80``어셈블리 명령어를 호출하고 소프트웨어 인터럽트를 발생하여 커널로 하여금 하던 일을 멈추고 인터럽트를 처리하도록 한다.
        2.  커널은 파라미터가 올바른지 확인하고 레지스터 값을 커널 메모리 공간에 복사하고 인터럽트 기술 표(IDT)를 참조하여 인터럽트를 처리한다.
5. Binary stripping
   1. Binary가 빌드된 후 strip유틸리티를 사용하여 관련된 정보, 심볼을 없애 바이너리 분석을 난독화한다.
6. Spoofing
   1. 다른 사람인 척 한다.
   2. 종류
      1. ARP Spoofing
         1. 네트워크 게이트웨이인 척
         2. 네트워크에는 HSRP(Hot Standby Router Protocol)기술이 있다. 두 라우터를 게이트웨이로 동작하게 하며, 가상 IP를 생성한다. 이 가상 IP주소는 두 라우터 사이를 왔다갔다 할 수 있어야 하는데, 어떤 ARP엔트리는 20분 타임아웃 시에만 업데이트를 한다. 이를 방지하고자 불필요한 ARP응답(Gratuitous ARP Response)를 보내는데, 이 패킷의 목적은 로컬 시스템의 ARP캐시를 업데이트하는 것이다. 이를 라우터가 하면 장점이 되지만 중간자(MITM: Man In The Middle)이 하면 ARP Spoofing이 된다. 두 사이의 중간자가 되면 서로 오가는 패킷을 가로챌 수 있다.
      2. DNS Spoofing
         1. DNS를 IP로 변환하는 과정을 조작
7. 스택의 동작 방식
   1. STACK(First-in, Last-out)
      1. 후입선출
   2. 메모리에서 각 프로세스는 자신의 스택을 메모리 스택 세그먼트 안에 갖고 있다. 가장 높은 메모리 주소에서 가장 낮은 메모리 주소 방향으로 스택이 늘어난다.
   3. 함수를 콜하면 EIP(Extended Instruction Pointer)가 스택에 저장되고 이가 복귀주소로 활용된다.
   4. 프롤로그(Prolog)
      1. 첫째로 호출한 프로그램의 EBP(Extended Base Pointer) 레지스터를 스택에 저장한다.
      2. 그리고 ESP(Extended Stack Pointer) 레지스터를 EBP에 저장한다.
      3. 그리고 ESP레지스터를 감소시켜 함수의 지역 변수용 공간을 만들고 구문을 실행할 기회를 얻게 된다.
   5. 에필로그(Epilog)
      1. 호출한 함수로 돌아가기 전 호출된 함수가 마지막으로 하는 일은 ESP를 EBP로 증가시켜서 스택을 지우는 것이다.
      2. 그 뒤에 저장된 EIP를 스택에서 팝해서 복귀한다.
   6. 버퍼 오버플로
      1. 변수를 지정하면 100프로 채워지지 않는다. 이 부분을 허용량 이상의 변수를 집어넣어서 오버플로를 일으킨다. 오버플로를 일으키면 EIP를 넘어서 다음 명령을 가리키는 영역을 침범한다. EIP는 실행할 다음 명령을 가리키고 함수가 실행된 다음 명령을 계속 실행하고자 함수 호출의 일부로 스택에 EIP의 복사본을 저장한다. 함수가 값을 반환할 때 저장된 EIP값에 영향을 미칠 수 있다면 손상된 EIP값을 스택으로부터 팝하여 EIP에 넣은 다음 이를 실행할 수 있다.
      2. 그렇다면 오버플로를 발생시키고 이 때 권한을 상승하는 등의 악성코드를 집어넣어서 강제로 권한을 올릴 수 있는 명령을 실행시킬 수 있게 된다.