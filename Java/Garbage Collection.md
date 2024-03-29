# Java Garbage Collection

Garbage Collection은 JVM이 자동으로 메모리 관리를 수행하는 기능 중 하나다. 프로그램에서 더 이상 사용하지 않는 메모리를 식별하고, 자동으로 반환하여 더 이상 사용하지 않는 메모리 누수를 방지한다.

## 가비지 컬렉션 과정

Java는 프로그램 코드에서 메모리를 명시적으로 지정하여 해제하지 않는다. 대신 가비지 컬렉터(Garbage Collector)가 더 이상 필요 없는 객체를 찾아 지우는 작업을 한다.

Java의 대부분의 객체는 금방 접근 불가능 상태가 되며, 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다. 이러한 조건 아래 가비지 컬렉터가 최대한 효율적으로 동작하기 위해 힙을 물리적으로 두 가지 영역으로 나누었다.

- Young 영역 : 새롭게 생성한 객체의 대부분이 여기에 위치한다. 대부분의 객체가 금방 접근 불가능한 상태가 되기 때문에 매우 많은 객체가 Young 영역에 생성되었다가 사라진다. 이 영역에서 객체가 사라질 때 Minor GC가 발생한다고 말한다.

- Old 영역 : 접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 여기로 복사된다. 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다. 이 영역에서 객체가 사라질 때 Major GC가 발생한다고 말한다.

영역별 데이터 흐름을 그림으로 살펴보면 다음과 같다.

![image](https://user-images.githubusercontent.com/66311161/232411073-0670567c-c1c1-4965-862d-b5537e7995f2.png)

## Young 영역의 구성

Young 영역은 3개의 영역으로 나뉜다. 

- Eden 영역
- Survivor (2개)

각 영역의 처리 절차는 다음과 같다.

1. 새로 생성한 대부분의 객체는 Eden 영역에 위치한다.
2. Eden 영역에서 GC가 한 번 발생한 후 살아남은 객체는 Survivor 영역 중 하나로 이동된다.
3. Eden 영역에서 GC가 발생하면 이미 살아남은 객체가 존재하는 Survivor 영역으로 객체가 계속 쌓인다.
4. 하나의 Survivor 영역이 가득 차게 되면 그 중에서 살아남은 객체를 다른 Survivor 영역으로 이동한다. 그리고 가득찬 Survivor 영역은 아무 데이터도 없는 상태로 된다.
5. 이 과정을 반복하다가 계속해서 살아남아 있는 객체는 Old 영역으로 이동하게 된다.

이렇게 Minor GC를 통해서 Old 영역까지 데이터가 쌓인 것을 간단히 나타내면 다음과 같다.

![image](https://user-images.githubusercontent.com/66311161/232411126-11142ca5-ebfd-4ea4-bb88-eee7335507df.png)

## Old 영역에 대한 GC

Old 영역은 기본적으로 데이터가 가득 차면 GC를 실행하며, GC 방식에 따라서 처리 절차가 달라진다. JDK 7 기준으로 5가지 방식이 있다.

- Serial GC
- Parallel GC
- Parallel Old GC
- Concurrent Mark & Sweep GC
- G1 GC






