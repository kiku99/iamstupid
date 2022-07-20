# Git 브랜칭 전략

## 대표적인 Git 브랜칭 전략

- git-flow
- github-flow

## git-flow

git flow는 브랜치를 크게 4가지로 나누어 개발하는 전략
- main branch
- feature branch
- release branch
- hotfix branch

가장 중심이 되는 브랜치는 master와 develop 브랜치이며, merge된 feature, release, hotfix브랜치는 삭제한다.

git-flow 전략은 주기적으로 배포를 해야하는 프로젝트에는 적합하지만, 브랜치가 많아 복잡하고 어떤 프로젝트에 따라서는 몇몇 브랜치가 애매한 포지션을 가질 수 있다.

![image](https://user-images.githubusercontent.com/66311161/174708250-c37c7ce3-702c-4155-9df5-240d8aa602d6.png)

## Main branch

master 브랜치와 develop 브랜치를 보통 메인 브랜치로 사용하며, 두 브랜치는 병행으로 유지한다.

![image](https://user-images.githubusercontent.com/66311161/174708411-e376c304-b166-45a6-a075-bd3c61eed88b.png)

### master
- 배포 가능한 상태만을 관리하는 브랜치

### develop
- 다음에 배포할 것을 개발하는 브랜치
- develop 브랜치는 통합 브랜치의 역할을 하며, 평소에는 이 브랜치를 기반으로 개발을 진행


## Supporting branch

feature 브랜치, release 브랜치, hotfix 브랜치를 보조 브랜치로 사용



### feature 브랜치

![image](https://user-images.githubusercontent.com/66311161/174708988-15ce2474-3804-4de7-b0a9-bc2d8ab86d8b.png)

- 기능을 개발하는 브랜치로, develop 브랜치로부터 분기
- feature 브랜치는 그 기능을 다 완성할 때까지 유지하고, 다 완성되면 develop 브랜치로  merge
- feature 브랜치는 보통 개발자 저장소에만 있는 브랜치고 origin애는 push하지 않는다

### release 브랜치

![image](https://user-images.githubusercontent.com/66311161/174737459-2407da73-6664-4808-8877-6244d1086bc6.png)

- develop 브랜치에 이번 버전이 포함되는 기능이 merge되었다면 QA를 위해 develop 브랜치에서부터 release 브랜치를 생성
- 배포를 위한 최종적인 버그 수정 등의 개발을 수행
- 배포 가능한 상태가 되면 master 브랜치로 병합시키고, 출시된 master 브랜치에 버전 태그를 추가
- release 브랜치에서 기능을 점검하며 발견한 버그 수정 사항은 develop 브랜치에도 적용해 주어야함. 그러므로 배포 완료 후 develop 브랜치에 대해서도 merge 작업을 수행

### hotfix 브랜치

![image](https://user-images.githubusercontent.com/66311161/174738185-d1f63763-192d-482e-9dba-4b2cf5ea467c.png)

- 배포한 버전에서 긴급하게 수정을 해야 할 필요가 있을 경우, master 브랜치에서 분기하는 브랜치
- 버그를 잡는 사람이 일하는 동안에도 다른 사람들은 develop 브랜치에서 하던 일을 계속할 수 있다
- 이 때 만든 hotfix 브랜치에서의 변경 사항은 develop브랜치에도 merge하여 문제가 되는 부분을 처리


## github-flow

git-flow 전략이 github에서 사용하기에는 복잡하다고 나온 브랜칭 전략으로, 흐름이 단순한 만큼 role도 단순하다. master 브랜치에 대한 role만 정확하다면 나머지 브랜치들에 대해서는 관여하지 않는다. 즉 hotfix 브랜치나 feature 브랜치를 구분하지 않는다.

![image](https://user-images.githubusercontent.com/66311161/174741065-9d475f7f-e9a5-47cf-912e-f3caa1fe8766.png)

### 사용법
### 1. master 브랜치는 어떤 때든 배포가 가능하다

- master 브랜치는 항상 최신 상태며, stable 상태로 product에 배포되는 브랜치
- 이 브랜치에 대해서는 엄격한 role과 함께 사용한다
- merge하기 전에 충분히 테스트를 해야한다. 테스트는 로컬에서 하는 것이 아니라 브랜치를 push하고 Jenkins로 테스트 한다

![image](https://user-images.githubusercontent.com/66311161/174741540-9ddacd64-4cfa-446e-a98e-23b957e18824.png)

## 2. master 브랜치에서 새로운일을 시작하기 위해 브랜치를 만든다면, 이름을 명확히 작성해야 한다

- 브랜치는 항상 master 브랜치에서 만든다
- git-flow와는 다르게 feature 브랜치나 develop 브랜치가 존재하지 않는다
- 새로운 기능을 추가하거나, 버그를 해결하기 위한 브랜치 이름은 자세하게 어떤 일을 하고 있는지에 대해서 작성해야 한다
- 커밋 메세지를 명확하게 작성하자

![image](https://user-images.githubusercontent.com/66311161/174742461-8aac50d9-18cc-49f6-80e6-39c0078a486f.png)

## 3. 원격지 브랜치로 수시로 push 해야 한다

- git-flow와 상반되는 방식
- 항상 원격지에 자신이 하고 있는 일들을 올려 다른 사람들도 확일할 수 있도록 해준다
- 이는 하드웨어에 문제가 발생해 작업하던 부분이 없어지더라도, 원격지에 있는 소스를 받아서 작업할 수 있도록 해준다

## 4. 피드백이나 도움이 필요할 때, 그리고 merge 준비가 완료되었을 때는 pull request를 생성한다

- pull request는 코드 리뷰를 도와주는 시스템
- 이것을 이용해 자신의 코드를 공유하고, 리뷰를 받는다
-  merge 준비가 완료되었다면 master 브랜치로 반영을 요구해야 한다

![image](https://user-images.githubusercontent.com/66311161/174743458-a2078cff-764f-4f67-bfc2-ff74ac3020de.png)

## 5. 기능에 대한 리뷰와 논의가 끝난 후 master로 merge한다

- 곧장 product로 반영이 될 기능이므로, 이해관계가 연결된 사람들과 충분히 논의 이후 반영하도록 한다
- 물론 CI도 통과해야 한다

![image](https://user-images.githubusercontent.com/66311161/174745379-59e70df3-a7b1-4dd0-a3eb-684e9bc4787e.png)

## 6. master로 merge되고 push되었을 때는, 즉시 배포되어야 한다

- github-flow의 핵심
- master로 merge가 일어나면 자동으로 배포가 되도록 설정해 놓는다

![image](https://user-images.githubusercontent.com/66311161/174745873-18cf9be5-aa4f-4ef7-87cb-543de5ff7dda.png)



