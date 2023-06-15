# Linux shell

shell이란 사용자 명령어 해석기. 사용자가 프롬프트에 입력한 명령을 해석해서 운영체제(커널)에게 전달한다.

- Bourne shell(sh) : AT&T 벨 연구소의 스티븐 본이 개발한 original shell
- C shell(csh, tcsh) : Bill Joy가 C언어의 기술을 넣어서 만든 shell. History, aliases, job control, vi command editing and completion 기능을 포함
- Korn shell(ksh) : David Korn이 기존 bourne shell에 C shell의 기능을 포함시켜 생성
- Bourne-again shell(bash) : csh, ksh이 가진 기능을 포함하면서 bourne shell과 호환성을 많이 높인 shell로 리눅스, Mac OS의 기본 shell이고 윈도우에서도 사용가능

~~~bash
cat /etc/shells - 사용 가능한 shell 리스트 확인하기

echo $SHELL - 현재 작업 shell 확인

sudo chsh [username] - 로그인 shell 변경
~~~

## Bash shell과 변수

shell의 변수란?

- 데이터를 넣는 그릇
- 선언할 필요없이 사용 가능
- 변수명 : 문자, 숫자, _(언더바)로 구성될 수 있지만, 시작은 반드시 문자나 _로 시작

변수 선언 : varname=value

~~~bash
fname=kiku
score=90
~~~

변수 확인 : echo $varname

~~~bash
echo $fname
echo $score
~~~

변수 제거 : unset varname

~~~bash
unset fname
unset score
~~~

shell 환경변수란?

- 동작 되는 프로그램에게 영향을 주는 변수

환경 변수 선언 : export varname=value

~~~bash
export NAME=kiku
echo $NAME
~~~

환경변수 확인 : env

~~~bash
env
~~~

기억해야할 환경변수

- PATH : shell이 명령어를 실행하는 위치를 가리킴
- HOME : 홈디렉토리의 경로. cd 명령 실행시 적용
- USER : 로그인 사용자 이름
- SHELL : 로그인 shell의 이름

## Bash shell의 rule

## Bash shell script

## Positional Parameters

## Input & Output

## Branching

## Looping

## Shell Script Example