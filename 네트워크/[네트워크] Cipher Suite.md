# Cipher Suite

SSL/TLS 암호화 통신에 사용할 여러가지 알고리즘들의 집합

## Cipher Suite의 구조

![image](https://user-images.githubusercontent.com/66311161/181185556-0f761291-d15a-4da0-8e9e-67ec606ded4e.png)


## 프로토콜

SSLv3, TLSv1, TLSv1.2 와 같이 암호화 통신에 사용할 프로토콜을 명시하는 부분이다. 일반적으로 SSLv3은 취약점으로 인해 브라우저에서 지원을 중단하고 있는 추세다.

## 키 교환

WITH 앞쪽 부분이 보통 키교환과 인증(인증서 검증)을 담당하는 부분이다. 키 교환 알고리즘은 RSA, DH, DHE, ECDH, ECDHE를 제공한다.

- RSA: 비대칭키를 이용한 키교환 방식
- DH: 디피 헬만(Diffie Hellman) 방식
- DHE: Ephermeral 을 지원하는 디피 헬만 (Diffie Hellman) 방식 (PFS, Perfect Foward Secrecy  지원)
- ECDH : Elliptic Curve Diffie Hellman, Propose Cheme 방식
- ECDHE : Elliptic Curve 및 Ephermeral 을 지원하는 디피 헬만 (Diffie Hellman) 방식 (PFS, Perfect Foward Secrecy  지원)

## 인증

키를 교환할 상대방이 내어준 인증서가 정말 내가 접속하고자 하는 상대방이 맞는지 상위 인증기관을 통하여 확인하게 되는데, 이 때 사용되는 알고리즘을 의미한다. 보통 RSA, DSS, ECDSA, ANON 등이 있다. 인증서를 만들때 인증서 서명 요청(CSR)을 작성하여 상위 인증기관에 요청하게 되는데, 이 때 선택한 알고리즘이 선택된다.

만약 인증서 생성시 사용한 CSR에 RSA알고리즘을 넣어서 제출했다면 Cipher Suite는 다음과 같이 선택 될 수 있다. 

- RSA : 키교환 및 인증을 모두 RSA 알고리즘을 이용
- DH-RSA : 키교환은 디피 헬만 (Diffie Hellman), 인증은 RSA
- ECDHE-RSA : 키교환은 ECDHE, 인증은 RSA

## 암호화

실제 데이터를 암호화하는 부분은 WITH 뒷쪽에 표현된 Cipher Suite 값을 이용해 처리한다. 공개키 알고리즘을 이용하여 대칭키를 만들어 공유한 이후 실데이터 암호화를 진행하게 되는데 이 때 사용되는 알고리즘이 3DED, AES, AES128등이 있다.

## 블록 암호 운용 방식

실데이터를 AES128 과 같은 알고리즘으로 암호화 할 때 실데이터를 암호화 하는 것이 아니라 블록 단위로 쪼개서 암호화 하게 된다. 이 때 암호화 된 암호문을 가지고 실데이터를 추측하는 것을 방지하기 위하여 특정한 블록 암호 운용방식을 선택하게 되는데 이것이 블록 암호 운용 방식이다. 

- CBC : Chipher Block Chaining, 암호 블록 체인 모드, CTR과 CBC-MAC을 조합하여 계산, 느림
- GCM : Galois/Counter Mode, 갈르와 카운터 모드, CTR과 GHASH를 조합하여 계산, 빠름

## 메시지 인증

블록 단위로 암호화 된 메시지들이 상대방이 암호화 한 것이 맞는지 확인하기 위해 무결성을 검증하게 되는데, 이 떄 사용되는 것이 메시지 인증 부분이다. 이를 보통 MAC(Message Authentication Code)라고 하는데, 여기에 해쉬 알고리즘(SHA, SHA256, SHA384, MD5)을 이용하기 때문에 HMAC이라고 부른다.

![image](https://user-images.githubusercontent.com/66311161/181185596-86566863-de78-4ea7-818e-bbe7feacba54.png)


