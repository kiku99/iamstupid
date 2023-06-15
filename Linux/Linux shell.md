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

## Bash shell의 rule

## Bash shell script

## Positional Parameters

## Input & Output

## Branching

## Looping

## Shell Script Example