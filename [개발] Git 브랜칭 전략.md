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

