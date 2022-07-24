# Node.js

## Node.js 란?

사전적 정의: 자바스크립트를 실행시키는 런타임 환경

V8 엔진의 등장과 함께 개발된 자바스크립트 런타임 환경

## Node.js의 특성

- 비동기 이벤트 주도
- 논 블로킹 I/O 모델

운영체제는 쓰레드 기반의 동시성 모델을 사용한다. 하지만 이런 방식은 이벤트 주도 방식에 비해 자원의 낭비가 발생하고 개발자가 사용하기 어려우며 dead lock이 발생하는 문제점이 있다. 따라서 Node.js는 싱글 쓰레드를 효율적으로 사용할 수 있는 Event Loop를 선택했다.

### Event Loop

- Timers 단계

setTimeout(), setInterval()같은 타이머 관련 함수를 처리

- Pending 단계

CONNECTION_ERROR 같은 이전 루프에서 마무리 되지 못한 I/O 콜백을 처리

- Idle, Prepare 단계

내부의 작업 수행, I/O 폴링 사전 준비

- Poll 단계

NETWORK_IO, FILE_IO 같은 새로운 I/O 이벤트를 가져와서 실행되며 대부분의 콜백들이 이 단계에서 처리됨

- Check 단계

Node의 API중 하나인 setImmediate()로 스케줄링된 콜백들을 처리

- Close 단계

소켓 종료 같은 close 콜백 처리

## Node.js의 내부 구조

- Node.js Core Library
- Node.js Bindings
- V8
- libuv

libuv를 이용해 비동기 작업을 시스템 커널에 위임하여 동작


