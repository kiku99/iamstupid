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

### Main branch

master 브랜치와 develop 브랜치를 보통 메인 브랜치로 사용하며, 두 브랜치는 병행으로 유지한다.

![image](https://user-images.githubusercontent.com/66311161/174708411-e376c304-b166-45a6-a075-bd3c61eed88b.png)

master
- 배포 가능한 상태만을 관리하는 브랜치

develop
- 다음에 배포할 것을 개발하는 브랜치
- develop 브랜치는 통합 브랜치의 역할을 하며, 평소에는 이 브랜치를 기반으로 개발을 진행


### Surporting branch

feature 브랜치, release 브랜치, hotfix 브랜치를 보조 브랜치로 사용



feature 브랜치

![image](https://user-images.githubusercontent.com/66311161/174708988-15ce2474-3804-4de7-b0a9-bc2d8ab86d8b.png)

- 기능을 개발하는 브랜치로, develop 브랜치로부터 분기
- feature 브랜치는 그 기능을 다 완성할 때까지 유지하고, 다 완성되면 develop 브랜치로  merge
- feature 브랜치는 보통 개발자 저장소에만 있는 브랜치고 origin애는 push하지 않는다


