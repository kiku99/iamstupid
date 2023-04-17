# 12 Factors app

최근 소프트웨어를 서비스 형태로 제공하는게 일반화 되면서, 웹앱 혹은 SaaS라고 부르게 되었다.
12 Factors app은 아래와 같은 특징을 가진 SaaS앱을 만들기 위한 방법론이다.

- 설정 자동화를 위한 절차를 체계화 하여 새로운 개발자가 프로젝트에 참여하는데 드는 시간과 비용을 최소화한다.
- OS에 따라 달라지는 부분을 명확히하고, 실행 환경 사이의 이식성을 극대화한다.
- 최근 등장한 클라우드 플랫폼 배포에 적합하고, 서버와 시스템의 관리가 필요없게 된다.
- 개발 환경과 운영 환경의 차이를 최소화하고 민첩성을 극대화하기 위해 지속적인 배포가 가능하다.
- 툴, 아키텍처, 개발 방식을 크게 바꾸지 않고 확장할 수 있다.

12 Fatctors 방법론은 어떤 프로그래밍 언어로 작성된 앱에도 적용할 수 있고, 백엔드 서비스(데이터베이스, 큐, 메모리 캐시)와 다양한 조합으로 사용할 수 있다.

## 1.코드베이스

### 버전 관리되는 하나의 코드베이스와 다양한 배포

- 각 Twelve-factor 앱은 각 코드베이스로 관리된다.
- 코드베이스는 Git, Mercurial, Subversion 같은 버전 컨트롤 시스템(VCS)을 사용하므로 변화를 추적하며, 버전 추적 데이터베이스, 즉 저장소(Repository)로 관리된다.
- 코드베이스와 앱 사이에는 항상 1대1 관계가 성립되어야 한다.
- 코드베이스가 여러개 있는 경우, 여러 앱으로 구성된 분산 시스템으로 간주한다. 분산 시스템의 개별 앱은 각각 Twelve-Factor를 따라야 한다. 따라서, 만일 여러 앱이 동일한 코드를 공유한다면 Twelve-Factor를 위반하는 것이다. → 이를 해결하려면 공유하는 코드를 라이브러리화 시키고, 해당 라이브러리를 종속성 매니저로 관리해야 한다.
- 앱의 배포는 여러 버전으로 관리할 수 있다. 배포는 실행중인 앱의 인스턴스를 가리킨다.
운영/QA/개발 등의 각 버전으로 나누어 앱을 관리하는 것은 앱의 배포를 다양화한 것으로 볼 수 있다.

## 2.종속성

### 명시적으로 선언되고 분리된 종속성

종속성이란 앱 개발과 실행에 필요한 라이브러리들에 대한 앱의 의존성을 의미한다. 모든 종속성은 (1)명시적으로 선언(manifest)되고 (2)실행 환경과 분리되어야 한다. 본 특징을 만족하기 위해서 각 프로그래밍 언어는 라이브러리 배포를 위한 패키징 시스템을 함께 제공한다. (ex. Perl-CPAN, Ruby-Rubygems)

장점은 다음과 같다.

- 개발 환경 구축이 쉬워진다. 종속성 확보를 위한 과정이 간소화되기 때문이다. 빌드 명령어를 입력하기만 하면 코드가 실행되기 때문이다.
- 종속성의 추가/수정/삭제 등의 관리가 용이해진다.
- 시스템 종류에 대해서 암시적으로 의존하지 않을 수 있다

## 3.설정

### 환경(environment)에 저장된 설정

여기서 설정이란, 배포의 종류마다 달라질 수 있는 환경 관련 항목을 대상으로 한다. (ex. 데이터베이스와의 연결 정보, Amazon S3 등의 외부 서비스 인증 정보, 호스트 이름)

위와 같은 환경 관련 설정은 코드와 분리되어야 한다. 대표적인 위반 사례는 코드에 상수로 위 설정을 저장하는 것이다.

- 방법: 설정을 환경 변수(envvars, env 등)에 저장하고, 각 배포마다 독립적으로 관리한다(ex. prod, test, dev, qa).
- 장점: 코드 변경 없이 각 배포에 대해서 쉽게 변경할 수 있다. 

## 4.백엔드 서비스

### 백엔드 서비스를 연결된 리소스로 취급

백엔드 서비스란, 애플리케이션 정상 동작 중 네트워크를 통해 이용하는 모든 서비스를 통칭한다. 

- 로컬로 주로 사용되던 서비스는 데이터 저장소(예: MySQL, CouchDB), 메시지 큐잉 시스템(예: RabbitMQ, Beanstalkd), 메일을 보내기 위한 SMTP 서비스 (예: Postfix), 캐시 시스템(예: Memcached) 등이 있다.
- 서드파티 서비스는 SMTP 서비스 (예: Postmark), 지표 수집 서비스 (예: New Relic, Loggly), 스토리지 서비스 (예: Amazon S3), API로 접근 가능한 소비자 서비스 (예: Twitter, Google Maps, Last.fm)등이 있다.

기존에는 로컬에 서비스를 포함시키던 경향과 비교할 때, 최근에는 서드파티에 의해서 제공되는 서비스를 이용하는 경우도 많다. 

Twelve-factor app은 로컬 서비스와 서드파티 서비스를 모두 구분 없이 애플리케이션과 연결된 동등한 리소스로 취급한다.

장점은 다음과 같다.

- 리소스 변경 시 코드를 수정하지 않아도 된다.
- 리소스는 자유롭게 배포에 연결되거나 분리되므로 이슈에 대응하기 용이하다.

## 5.빌드, 릴리즈, 실행

### 철저하게 분리된 빌드와 실행 단계

코드베이스는 3 단계를 거쳐 배포된다.

1. 빌드 단계는 저장소의 코드로부터 종속성을 결합하여 실행 가능한 번들로 변환시킨다. 
2. 릴리즈 단계에서는 빌드 단계에서 만들어진 빌드와 배포의 환경 설정을 결합한다. 완성된 릴리즈는 빌드와 설정을 모두 포함하며 실행 환경에서 바로 실행될 수 있도록 준비된다.
3. 실행 단계(런타임이라고도 하는)에서는 선택된 릴리즈에 대한 애플리케이션 프로세스의 집합을 시작하고 애플리케이션을 실행 환경에서 돌아가도록 한다. 코드 베이스는 빌드가 되고, 빌드는 설정과 조합되어 릴리즈가 된다.

Twelve-Factor App은 빌드, 릴리즈, 실행 단계를 엄격하게 서로 분리한다. 예를 들어, 실행 단계에서 코드 또는 종속성을 변경할 수 없다.

특징은 다음과 같다.

- 배포 도구는 일반적으로 릴리즈 관리 도구를 제공한다. 각 릴리즈는 타임스탬프 등으로 구분된다.
- 이전 릴리즈로 되돌리는 롤백 기능이 존재하여 배포 관리가 용이하다.

## 6.프로세스

### 애플리케이션을 하나 혹은 여러개의 무상태(Stateless) 프로세스로 실행

실행 환경에서 앱은 하나 이상의 프로세스로 실행된다.

Twelve-Factor앱의 실행 프로세스는 stateless로써, 앱의 운영 상 유지되어야 할 모든 데이터는 프로세스 내 메모리가 아닌 데이터베이스와 같은 안정된 백엔드 서비스에 저장되어야 한다.

따라서 각 인스턴스는 메모리 파일 등을 공유할 필요가 없도록 설계해야 하며, 인스턴스가 재실행 될 때 local file, session과 같은 상태 정보는 모두 초기화되어야 한다.

- 특징 : 메모리/파일을 사용할 경우 단일 트랜잭션 내에서 읽고, 쓰고 등의 모든 작업을 처리한다.
- 세션 상태 데이터의 경우 Memcached 또는 Redis와 같은 데이터 저장소에 저장한다.

## 7.포트 바인딩

### 포트 바인딩을 사용해서 서비스를 공개함

Twelve-Factor 웹 앱은 포트를 바인딩하여 HTTP 등의 각종 프로토콜을 통해 요청을 받고 서비스를 제공한다.

- 로컬 개발 환경에서는 http://localhost:5000과 같은 주소를 통해 개발자가 애플리케이션 서비스에 접근할 수 있다.
- 배포 시에는 공개된 호스트명으로 들어온 요청을 바인딩된 포트를 통해 웹 프로세스에 전달한다.

특징은 하나의 앱이 다른 앱을 위한 백엔드 서비스가 될 수 있다.

## 8.동시성(Concurrency)

### 프로세스 모델을 통한 확장

모든 컴퓨터 프로그램은 실행되면 하나 이상의 프로세스로 표현된다. 웹 애플리케이션은 다양한 프로세스 실행 형태를 취해왔다. 예를 들어, PHP 프로세스는 Apache의 자식 프로세스로 실행되며, request의 양에 따라 필요한 만큼 시작된다. 자바 프로세스들은 반대 방향에서의 접근법을 취한다. JVM은 시작될 때 큰 시스템 리소스(CPU와 메모리) 블록을 예약하는 하나의 거대한 부모 프로세스를 제공하고, 내부 쓰레드를 통해 동시성(concurrency)을 관리한다. 두 경우 모두 실행되는 프로세스는 애플리케이션 개발자에게 최소한으로 노출된다.

Scale는 실행되는 프로세스의 갯수로 표현되고, Workload Diversity는 프로세스의 타입으로 표현된다.

프로세스의 타입과 각 타입별 프로세스의 갯수의 배치를 프로세스 포메이션이라고 한다. 런타임 VM 내부의 쓰레드나 EventMachine, Twisted 또는 Node.js의 async/evented 모델처럼 개별 프로세스가 내부적으로 동시에 처리하는 시스템은 개별 VM이 커지는 수직 확장적인 특징이 있다. 이에 비해서 위 모델과 같이 역할에 따라서 적당한 크기의 독립적인 프로세스가, 필요에 의해서 유연하게 확장되도록 설계된 모델은 수평적으로 확장 가능하다. 

장점은 개발자는 애플리케이션의 작업을 적절한 프로세스 타입에 할당함으로서 다양한 작업 부하를 처리할 수 있도록 설계할 수 있다. 예를 들어 HTTP 요청은 웹 프로세스가 처리하며, 시간이 오래 걸리는 백그라운드 작업은 worker 프로세스가 처리하도록 한다.

특징은 다음과 같다.

- 데몬화/PID 파일를 이용하여 프로세스를 관리하지 않는다.
- OS의 프로세스 관리자(예: systemd)나 클라우드 플랫폼의 분산 프로세스 매니저, 혹은 Foreman 같은 툴에 의존하여 아웃풋 스트림 관리, 프로세스 충돌 대응, 재시작과 종료 등을 처리한다.

## 9.폐기 가능(Disposability)

### 빠른 시작과 그레이스풀 셧다운(graceful shutdown)을 통한 안정성 극대화

프로세스는 프로세스 매니저로부터 SIGTERM 신호를 받았을 때 그레이스풀 셧다운(graceful shutdown)을 한다. 웹프로세스의 그레이스풀 셧다운 과정에서는 서비스 포트의 수신을 중지하고(그럼으로써 새로운 요청을 거절함), 현재 처리 중인 요청이 끝나길 기다린 뒤에 프로세스가 종료된다. 

특징은 다음과 같다.

- Twelve-Factor App의 프로세스는 간단하고 안전하게 폐기 가능하다. (=Graceful shutdown)
- 즉, 프로세스는 DB Lock 등의 우려 없이 바로 시작하거나 종료될 수 있다. 
- 신축성 있는 확장과 코드나 설정의 변화를 빠르게 배포하는 것이 쉬워지고, production 배포를 안정성 있게 한다.
- SIGTERM 뿐 아니라 하드웨어 에러에 의한 갑작스러운 종료에 대해서도 안정적이다.

구현 방법은 다음과 같다.

- worker 프로세스의 경우 현재 처리중인 작업을 작업 큐로 되돌리는 방법으로 구현된다.
- Lock-based 시스템들은 작업 레코드에 걸어놨던 lock을 풀고 종료되어야 한다.
- 결과를 트랜잭션으로 감싸거나 요청을 멱등(idempotent)하게 함으로써 모든 작업이 재입력 가능(reentrant)하도록 구현한다.

## 10.dev/prod 일치

### development, staging, production 환경을 최대한 비슷하게 유지

development, staging, production 환경을 최대한 비슷하게 유지한다.

- 개발 환경: 애플리케이션의 개발자가 직접 수정하는 로컬의 배포
- production 환경: 최종 사용자가 접근하게 되는 실행 중인 배포
- 12 factors app은 개발 환경과 production 환경의 차이를 작게 유지하여 지속적인 배포가 가능하도록 디자인되어야 한다.

배경은 이렇다.

서비스 간의 불일치가 개발 환경과 스테이징 환경에서는 동작하고 테스트에 통과된 코드가 production 환경에서의 오류를 일으킬 수 있다. 이는 지속적인 배포를 방해하며, 앱의 라이프사이클을 고려할 때 지속적인 배포의 둔화가 발생시키는 손해는 매우 크다. 특히, 데이터베이스, 큐잉 시스템, 캐시와 같은 백엔드 서비스는 dev/prod 일치가 중요한 영역 중 하나이다.

특징은 다음과 같다.

- 시간의 차이를 최소화: 개발자가 작성한 코드는 몇 시간 또는 몇 분 후에 배포될 수 있어야 한다.
- 담당자의 차이를 최소화: 코드를 작성한 개발자들이 배포와 production에서의 모니터링 역할을 동시 수행할 수 있어야 한다.
- 툴의 차이를 최소화: 개발과 production 환경을 최대한 비슷하게 유지해야 한다.

## 11.로그

### 로그를 이벤트 스트림으로 취급

로그는 모든 실행중인 프로세스와 백그라운드 서비스의 아웃풋 스트림으로부터 수집된 이벤트가 시간 순서로 정렬된 스트림이다. 각 프로세스는 이벤트 스트림을 버퍼링 없이 stdout에 출력하고 12 Factors App은 로그 파일을 작성하거나, 관리하지 않는다.

방법은 다음과 같다.

1. 스테이징이나 production 배포에서는 각 프로세스의 스트림은 실행 환경에 의해서 수집된다.
2. 그 다음, 앱의 다른 모든 스트림과 병합되어 열람하거나 보관하기 위한 저장소로 전달된다.
3. 목적지들은 앱이 열람하거나 설정할 수 없고, 실행 환경에 의해서 완벽하게 관리된다. (예: Logplex, Fluentd 활용)

특징이라고 하면, 이러한 시스템은 장기간에 걸쳐 앱의 동작을 조사할 수 있는 강력함과 유연성을 가지게 된다.

예시는 다음과 같다.

- 과거의 특정 이벤트를 찾기
- 트렌드에 대한 거대한 규모의 그래프 (예: 분당 요청 수)
- 유저가 정의한 휴리스틱에 따른 알림 (예: 분당 오류 수가 임계 값을 넘는 경우 알림을 발생시킴)

## 12.Admin 프로세스

### admin/maintenance 작업을 일회성 프로세스로 실행

앱의 일반적인 기능들(예: Web request의 처리)을 처리하기 위한 프로세스들의 집합과는 별도로 개발자들은 종종 일회성 관리나 유지 보수 작업을 필요로 하는데, 이러한 작업은 스크립트 등의 일회성 프로세스로 실행되어야한다.

- 데이터베이스 마이그레이션 (예: Django에서 manage.py migrate, Rail에서 rake db:migrate)
- 임의의 코드를 실행하거나 라이브 데이터베이스에서 앱의 모델을 조사하기 위해 콘솔 실행(REPL Shell)
- 대부분의 언어에서는 인터프리터를 아무런 인자 없이 실행하거나(예: python, perl) 별도의 명령어로 실행(예: ruby의 irb, rails의 rails console)할 수 있는 REPL를 제공한다.
- 앱 저장소에 커밋된 일회성 스크립트의 실행 (예: php scripts/fix_bad_records.php)

특징은 다음과 같다.

- 일회성 admin 프로세스는일반적인 앱 기능 프로세스들과 동일한 환경에서 실행되어야 한다.
- 일회성 admin 프로세스들은 릴리즈를 기반으로 실행된다.
- 해당 릴리즈를 기반으로 돌아가는 모든 프로세스처럼 같은 코드베이스와 설정를 사용해야 한다.
- admin 코드는 동기화 문제를 피하기 위해 애플리케이션 코드와 함께 배포되어야 한다.
- 일반적인 프로세스와 마찬가지로 종속성 분리 기술이 사용되어야 한다.
- 위와 같은 특징이 반영되면, 개발자는 ssh나 배포의 실행 환경에서 제공하는 다른 원격 명령어 실행 메커니즘을 사용하여 admin 프로세스를 실행할 수 있게 된다.