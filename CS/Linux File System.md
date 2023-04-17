# Linux File System

- file : 데이터를 담는 그릇
- file system : file을 관리하는 시스템
- file system은 파일을 관리할 정보가 필요하다
- directory : 파일을 편하게 관리하기 위한 도구
- directory entry : directory를 표현하는 자료구조

![image](https://user-images.githubusercontent.com/66311161/169558332-1d1f41bc-1023-467d-a450-4857a5f165ae.png)

inode number(32bit) directory length(16bit) name length(8bit) file type(8bit) file name(80) 으로 구성(linux ext3 file system)

## I-node

파일에 대한 정보(meta data)를 가진 일종의 데이터. 파일이나 디렉토리는 고유한 i-node를 가진다

### I-node의 구조

![image](https://user-images.githubusercontent.com/66311161/169557256-dfcd8913-fb7d-480d-94b5-f23f3bbb5b0d.png)

- 파일 모드(권한)
- 링크 수
- uid
- gid
- 파일 크기
- 파일이 사용하는 block 수
- 최근 수정한 시간
- 최근 접근된 시간
- 최근 변경된 시간
- block pointer

### block pointer

- direct block pointer
- indirect block pointer
- double indirect block pointer
- triple indirect block pointer

## Link

- symbolic link(soft link)

![image](https://user-images.githubusercontent.com/66311161/169557344-6003c641-29ce-40df-9b49-853c4cbe7988.png)

- hard link

![image](https://user-images.githubusercontent.com/66311161/169557427-f08f169e-12cd-497c-83e8-ff4a9580a600.png)


## permission

특정 파일이나 디렉터리에 대하여 읽기, 기록하기, 삭제하기 등의 권한을 설정해 놓은 것으로 다중 사용자 운영체제에서 파일의 접근권한과 보호 등을 위하여 반드시 필요한 것

- user
- group
- others

![image](https://user-images.githubusercontent.com/66311161/169557487-3974e783-a106-4520-9ce1-2b20e57efa8f.png)


r(read), w(write), x(excute)를 2진수로 표현

rwx = 4+2+1 = 7

ex) 754 = rwx(user) r-x(group) r--(others)

## mount

Mount란 하드디스크 파티션, CD/DVD, USB 메모리 등 물리적인 장치를 특정 위치에 연결시키는 과정

윈도우 운영체제에서는 PnP 기능에 의해 자동으로 주변 장치를 인식하기 때문에 직접 마운트 작업을 하지 않아도 되지만 리눅스 환경에서는 각각의 파티션들을 마운트 해주어야 함

## file allocation

디스크에 파일을 저장하기 위해 공간을 관리해야 함

- contiguous allocation
- linked allocation
- FAT
- indexed allocation
- multilevel index

### Contiguous Allocation

디스크에 연속적으로 file block을 할당

특정 파일을 append 할 때 여유공간이 없다면 충분한 공간이 있는 위치로 이동시킨 뒤 확장

Block 들을 옮기고 지우는 방식은 copy & paste를 하게 되는데, 
그러면 필연적으로 disk access 횟수가 늘어나게 되므로 매우 느림

![image](https://user-images.githubusercontent.com/66311161/169557871-2502beea-d382-4cd8-a746-b321c5bf7590.png)

### Linked Allocation

Contiguous Allocation의 단점을 보완

Data block이 디스크 상에서 흩어져 있지만 link를 통해 연결

마지막 블록의 link에는 끝임을 표시하는 nil(-1)이 저장

Linked list의 단점인 sequential access 존재

![image](https://user-images.githubusercontent.com/66311161/169558489-50e24760-29f0-4ead-a945-e58e8153bee8.png)

### FAT

특정 파일의 link정보를 저장

Link 정보를 따로 저장하므로, disk의 추가 용량이 필요 없음

시작 block주소만 알고 있다면 FAT를 탐색하여 이후 block의 주소를 알 수 있다

하지만 table을 위한 공간이 따로 필요한데, 이를 해결하기 위해 main memory의 cache에 해당 table을 저장

![image](https://user-images.githubusercontent.com/66311161/169559463-48187182-11cc-4eab-a47c-48a0ba1f594d.png)

### Indexed Allocation


하나의 block이 table역할을 함

 file date block이 한 두개 정도인 경우라도 무조건 index block을 할당해야 하므로, 공간 낭비 발생

큰 용량의 file을 저장하기 힘들다는 단점 존재

![image](https://user-images.githubusercontent.com/66311161/169559586-07afda8f-5d21-45a3-90fc-59d29d99a244.png)

### Multilevel Index

12개의 direct block과 하나의 single, double, triple indirect block을 가지는 방식

![image](https://user-images.githubusercontent.com/66311161/169559667-fc61a867-e1a3-4c67-9e5d-1b0dcbf0e255.png)







