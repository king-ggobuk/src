# 리눅스(CentOS) 서버 IP 설정 방법!

# 

오늘은 리눅스(CentOS) 서버의 IP를 설정하는 방법에 대하여 알아보겠습니다.

사실 설정이라는 말보다 고정이라는 말로 표현하는게 맞겠습니다.

이 방법은

1. **서버를 새로 구축**하였거나

2. **기존의 서버 IP를 변경**해야 할 일이 생겼을 때, IP를 고정으로 설정하기 위해 많이 하는 작업이니 아래와 같은 절차로 진행하면 되겠습니다.

**1. 서버에서 사용하고 있는 네트워크 인터페이스명 확인**

- 가장 먼저 서버에서 어떤 네트워크 인터페이스명을 사용하고 있는지 확인해야 합니다. 네트워크 인터페이스명은 보통 eth0, eno1등.. 다르게 나오기 때문에 꼭 확인해야 하는 작업입니다.

**2. Ip addr show 명령어로 네트워크 인터페이스명 확인**

# ip addr show

- 위와 같은 명령어를 입력하여 보면 네트워크 인터페이스가 UP인지 DOWN인지 확인할 수 있습니다.

**- UP : 네트워크 선과 서버가 연결되어 있다는 의미**

**- DOWN : 네트워크 선과 서버가 연결되어 있지 않다는 의미**

****

![https://postfiles.pstatic.net/MjAyMTAxMDhfMTA2/MDAxNjEwMDgzNDIxOTgw.vl9mqsrUm08QyHy5exs_tymcMmGyNzsoWBKDxs-sMfkg.4wO0KlQ2STcTxYEFiQH0WSiqbBHbmj8N_wNkqkv_O0Mg.PNG.90crew/image01.png?type=w773](https://postfiles.pstatic.net/MjAyMTAxMDhfMTA2/MDAxNjEwMDgzNDIxOTgw.vl9mqsrUm08QyHy5exs_tymcMmGyNzsoWBKDxs-sMfkg.4wO0KlQ2STcTxYEFiQH0WSiqbBHbmj8N_wNkqkv_O0Mg.PNG.90crew/image01.png?type=w773)

※ 위와 같이 보시면 eth0의 인터페이스 state가 UP 상태입니다.

우리는 이 **eth0 인터페이스의 IP를 설정**하도록 하겠습니다.

**3. CentOS IP 수정 디렉토리**

- CentOS의 IP를 수정하는 디렉토리는

/etc/sysconfig/network-scripts

입니다.

/etc/sysconfig/network-scripts 하위의 파일들을 보면 아래 사진과 같습니다.

![https://postfiles.pstatic.net/MjAyMTAxMDhfNTcg/MDAxNjEwMDgzNTYzMDYz.XFV2Yleky26b5XkEttsYDsKrs3T9eMxn0-Zl5SyJZ70g.PQ_KlcXL3yNy5tbVIsdHKryyqKefzCXN27OrPAaAmgEg.PNG.90crew/image02.png?type=w773](https://postfiles.pstatic.net/MjAyMTAxMDhfNTcg/MDAxNjEwMDgzNTYzMDYz.XFV2Yleky26b5XkEttsYDsKrs3T9eMxn0-Zl5SyJZ70g.PQ_KlcXL3yNy5tbVIsdHKryyqKefzCXN27OrPAaAmgEg.PNG.90crew/image02.png?type=w773)

/etc/sysconfig/network-scripts 하위의 파일 목록

(ifcfg-eth0.bak 파일은 제가 개인적으로 백업한 파일입니다.)

보통은 ifcfg-[네트워크 인터페이스명]으로 이루어져 있기 때문에 여기서는 **ifcfg-eth0 파일을 수정**하면 됩니다.

**4. IP 입력**

- 이제 /etc/sysconfig/network-scripts 디렉토리의 ifcfg-eth0 파일을 **vi 에디터로 수정**해보록 하겠습니다!!

(저는 보통 작업 전에 혹시 모를 오타나 정상적으로 반영이 되지 않을 경우를 대비하여 파일 백업을 해놓는 편이기 때문에 여러분들도 백업하시는 것을 추천합니다..!)

**5. 파일 백업**

- 백업은 **cp 명령어**로 진행합니다.

# cp /etc/sysconfig/network-scripts/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0.bak

**6. 파일 수정**

- 파일은 아까 말씀드렸듯이 **vi 에디터**로 수정합니다.

# vi /etc/sysconfig/network-scripts/ifcfg-eth0

- vi 화면으로 들어가게 되면, 아래와 같이 IP 고정작업을 할 수 있습니다.

![https://postfiles.pstatic.net/MjAyMTAxMDhfMTYy/MDAxNjEwMDgzODk2OTAy.muqsm_AwTQhkHvroFRmEIoViBZnAF4_kKO2DTD4EkuMg.1TBlff_5dR41Pw_KrjqLyvhOdlcM3EY65c6_jFV1f0og.PNG.90crew/image03.png?type=w773](https://postfiles.pstatic.net/MjAyMTAxMDhfMTYy/MDAxNjEwMDgzODk2OTAy.muqsm_AwTQhkHvroFRmEIoViBZnAF4_kKO2DTD4EkuMg.1TBlff_5dR41Pw_KrjqLyvhOdlcM3EY65c6_jFV1f0og.PNG.90crew/image03.png?type=w773)

여기서 ****
**BOOTPROTO,** 
**ONBOOT,** 
**IPADDR,** 
**NETMASK,** 
**GATEWAY,** 
**DNS1** 
부분을 수정하도록 하겠습니다.

- **유동적인 IP**를 설정할 때,

BOOTPROTO에는 **보통 dhcp**로 되어있는데,

지금은 **고정 IP**를 설정할 것이기 때문에, **none** 또는 **static**을 입력하시면 됩니다.

BOOTPROTO=none

- **ONBOOT 옵션**은 서버가 켜졌을 때,

설정이 되냐를 물어보는 것이므로 **yes**로 설정해야 합니다.

ONBOOT=yes

- **IPADDR 옵션**에는 **서버에 사용할 IP**를 입력하면 됩니다.

IPADDR=192.168.35.90

- **NETMASK**에는 **넷 마스크 주소**를 입력하시면 됩니다.

NETMASK=255.255.255.0

- **GATEWAY**에는 **게이트웨이 주소**를 입력하시면 됩니다.

GATEWAY=192.168.35.1

- **DNS1, DNS2**에는 **각각 DNS 주소**를 입력해주시면 됩니다.

(DNS 주소를 1개 사용하는거면, DNS1만 입력해주어도 무방합니다.)

DNS1=8.8.8.8

- 위와 같이 설정해 주었다면 IP 설정작업은 끝이 났습니다!!

이제 네트워크 데몬을 재시작하여, IP가 변경되었는지 확인하면 됩니다.

**7. 네트워크 데몬 재시작**

- 네트워크 데몬 재시작 명령어는

**systemctl restart network** 또는

**service network restart**라고 입력하면 되는데,

(저의 CentOS 버전이 8이 넘어가다 보니, network라는 데몬이 없더군요.)

찾아보니 저는 NetworkManager라는 데몬이 있었습니다.

그래서 저는 **systemctl restart NetworkManager** 또는 **service NetworkManager restart** 라고 입력하였습니다.

# systemctl restart NetworkManager

또는

# service NetworkManager restart

**8. IP 변경 확인**

- 네트워크 데몬까지 재시작하였다면, 이제 IP가 정상적으로 설정되었는지 확인하면 됩니다.

IP 확인은 **ifconfig 명령어**로 확인하겠습니다.

# ifconfig

![https://postfiles.pstatic.net/MjAyMTAxMDhfMzEg/MDAxNjEwMDg1MzE5ODEy.edbhe1-3b7Ykf-XhIrG6ocBkVyXoRJDp6IHm-QaNL0Ag.WvyL2sl9VNIt1WO-uJl9_g1LMW4EfGInO8ljxmdkWt8g.PNG.90crew/image04.png?type=w773](https://postfiles.pstatic.net/MjAyMTAxMDhfMzEg/MDAxNjEwMDg1MzE5ODEy.edbhe1-3b7Ykf-XhIrG6ocBkVyXoRJDp6IHm-QaNL0Ag.WvyL2sl9VNIt1WO-uJl9_g1LMW4EfGInO8ljxmdkWt8g.PNG.90crew/image04.png?type=w773)

설정된 IP 주소

- 위의 이미지와 같이 **eth0의 인터페이스 IP**가 **192.168.35.90**으로 설정되었습니다!

- CentOS의 IP 설정은 이렇게 진행하면 되겠습니다! 지금까지 90crew의 River였습니다.
