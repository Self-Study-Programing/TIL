# git-flow

이는 우아한 형제들 기술블로그에 쓰여진 글을 중점으로 git-flow를 설명해보겠다.

먼저 우아한 형제들에서는 작업할 때 서로 간의 약속이 있다.

1. 작업을 시작하기 전에 JIRA 티켓을 생성합니다.
2. 하나의 티켓은 되도록 하나의 커밋으로 합니다.
3. 커밋 그래프는 최대한 단순하게 가져갑니다.
4. 서로 공유하는 브랜치의 커밋 그래프는 함부로 변경하지 않습니다.
5. 리뷰어에게 꼭 리뷰를 받습니다.
6. 자신의 Pull Request는 스스로 merge 합니다

지금부터 git-flow에 대해 알아보겠다.

## Git-flow 전략

Git-flow에는 5가지 종류의 브랜치가 존재한다. 항상 유지되는 메인 브랜치들(master, develop)과 일정 기간 동안만 유지되는 보조 브랜치들(feature, release, hotfix)이 있다.

- master : 제품으로 출시될 수 있는 브랜치
- develop : 다음 출시 버전을 개발하는 브랜치
- feature : 기능을 개발하는 브랜치
- release : 이번 출시 버전을 준비하는 브랜치
- hotfix : 출시 버전에서 발생한 버그를 수정 하는 브랜치

![gitflow](./img/gitflow.png)

처음에는 master와 develop 브랜치가 존재한다. 물론 develop 브랜치는 master에서부터 시작된 브랜치이다. develop 브랜치에서는 상시로 버그를 수정한 커밋들이 추가된다. 새로운 기능 추가 작업이 있는 경우 develop 브랜치에서 feature 브랜치를 생성한다. feature 브랜치는 언제나 develop 브랜치에서부터 시작하게 된다. 기능 추가 작업이 완료되었다면 feature 브랜치는 develop 브랜치로 merge 된다. develop에 이번 버전에 포함되는 모든 기능이 merge 되었다면 QA를 하기 위해 develop 브랜치에서부터 release 브랜치를 생성한다. QA를 진행하면서 발생한 버그들은 release 브랜치에 수정된다. QA를 무사히 통과했다면 release 브랜치를 master와 develop 브랜치로 merge 한다. 마지막으로 출시된 master 브랜치에서 버전 태그를 추가한다.

실제로 우아한 형제들에서 사용하는 방법을 알아보자

아래의 Repository와 Branch는 앞으로 설명을 할 때 나오기 때문에 알아 두시고 가면 한결 수월하게 보실 수 있을 거라고 생각합니다.

- Repositories
  1. upstream (Upstream Repository)
  2. origin (Origin Repository)
- Branches
  1. feature-user (사용자 관련 기능을 구현하는 feature branch)
  2. bfm-100_login_layout (사용자 관련 기능 중 레이아웃 작업 branch)

## 티켓 처리하기

Github-flow에서 Git-flow로 변경됐지만 하나의 티켓을 처리하는 방법은 이전과 비슷합니다. 다만 티켓을 처리하는 개발자는 Github-flow를 하고 있을 때와는 다르게 관리되는 브랜치들이 늘어남에 따라 어느 브랜치에서 작업을 해야 하는지 항상 주의해야 합니다.

앞서 ‘작업을 할 때 지켜야 할 서로 간의 약속’에서 ‘하나의 티켓은 되도록 하나의 커밋으로 한다’라고 했습니다. 그래서 기능을 구현하기 전에 여러 개의 티켓으로 작업을 먼저 나누게 됩니다. 나눠진 작업 티켓 중 ‘로그인 레이아웃 생성’이라는 티켓이 있고 이 티켓을 처리한다고 가정하고 살펴보겠습니다.

1.  upstream/feature-user 브랜치에서 작업 브랜치(bfm-100_login_layout)를 생성합니다.

        (feature-user)]$ git fetch upstream
        (feature-user)]$ git checkout -b bfm-100_login_layout –track upstream/feature-user

2.  작업 브랜치에서 소스코드를 수정합니다. (뚝딱뚝딱 :hammer:)

3.  작업 브랜치에서 변경사항을 커밋합니다. (보통은 vi editor에서 커밋 메세지를 작성 함)
    (bfm-100_login_layout)]$ git commit -m "BFM-100 로그인 화면 레이아웃 생성"

4.  만약 커밋이 불필요하게 어려 개로 나뉘어져 있다면 squash를 합니다. (커밋 2개를 합쳐야 한다면)
    (bfm-100_login_layout)]$ git rebase -i HEAD~2

5.  작업 브랜치를 upstream/feature-user에 rebase합니다.
    (bfm-100_login_layout)]$ git pull –rebase upstream feature-user

6.  작업 브랜치를 origin에 push합니다.
    (bfm-100_login_layout)]$ git push origin bfm-100_login_layout

7.  Github에서 bfm-100_login_layout 브랜치를 feature-user에 merge하는 Pull Request를 생성합니다.
8.  같은 feature를 개발하는 동료에게 리뷰 승인을 받은 후 자신의 Pull Request를 merge합니다. 만약 혼자 feature를 개발한다면 1~2명의 동료에게 리뷰 승인을 받은 후 Pull Request를 merge합니다.
    위의 절차에서 4, 5번의 작업을 수행하는 이유는 커밋 그래프를 단순하게 가져가고 의미 있는 커밋들로 관리하기 위해서입니다.

4번 작업을 예로 들면, ‘BFM-100 로그인 화면 레이아웃 생성’ 작업을 할 때 로그인 화면의 레이아웃을 생성한 커밋 하나와, view의 약간의 간격을 조정한 커밋 하나, 그리고 view의 id를 변경한 커밋 하나, 이렇게 3개의 커밋으로 분리된 상태입니다. 이 3개의 커밋이 그 의미를 나눌 필요가 없거나 코드리뷰를 도와주지도 못한다면 커밋을 분리하는 것은 불필요하다고 판단하고 하나의 커밋으로 합치게 됩니다. 물론 항상 하나의 커밋으로 합쳐야만하는 것은 아닙니다. 하나의 티켓에 대한 작업이라도 커밋이 분리되어 있는 게 낫다고 생각이 든다면 2개 이상의 커밋으로 나눌 수도 있습니다. 그러나 대부분은 티켓을 더 작게 나누지 못한 경우일 가능성이 높습니다.

5번 작업도 예를 들어보면, 동료와 같이 같은 기능을 개발하면 하나의 feature 브랜치에 커밋을 하게 됩니다. 서로 같은 커밋에서 시작했다가 feature 브랜치에 하나씩 merge 되기도 하고 얽히고설켜서 merge 되기도 합니다. 그러면 커밋 그래프가 복잡해지고 이력 확인을 할 때도 어렵게 됩니다. 그래서 커밋을 순차적으로 만들기 위해서 작업한 커밋이 feature의 최신 상태에서 시작하도록 rebase를 수행합니다.

아래 그래프를 보시면 rebase를 했을 때 그래프가 얼마나 단순해지는지 볼 수 있습니다.

![rebase](./img/gitflowrebase.png)

## develop 변경사항을 feature로 가져오기 (Optional)

작업을 할 때 브랜치의 수명은 되도록 짧게 가져가는 게 좋지만, feature 브랜치에서 기능을 완료하는데 해야 할 작업들이 많아서 오래 걸리는 경우 들이 있습니다. 그러다 보면 develop에 추가된 기능들이 필요한 경우가 종종 생기게 됩니다. 그럴 때는 feature 브랜치에 develop의 변경사항들을 가져와야 합니다.

1. feature-user 브랜치에 upstream/develop 브랜치를 merge 합니다.
   (feature-user)]$ git fetch upstream
   (feature-user)]$ git merge –no-ff upstream/develop

2. upstream/develop의 변경사항이 merge된 feature-user를 upstream에 push 합니다.
   (feature-user)]$ git push upstream feature-user

## 완료된 기능을 이번 출시 버전에 포함시키기

드디어 feature-user 브랜치에서 작업하던 기능이 완료되었습니다. 이젠 feature 브랜치를 이번 출시 버전에 포함시키기 위해서 develop에 merge 해야 합니다.

1. develop 브랜치에 upstream/feature-user 브랜치를 merge 합니다.
   (develop)]$ git fetch upstream
   (develop)]$ git merge –no-ff upstream/feature-user

2. upstream/feature-user 기능이 merge된 develop를 upstream에 push 합니다.
   (develop)]$ git push upstream develop

## QA 시작하기

이번 버전에 포함되어야 할 기능들이 모두 완료되었습니다. 이제부터 출시 담당자가 해야 할 일이 많습니다. 출시 담당자는 QA를 시작하기 위해 먼저 release 브랜치를 생성하고 upstream에 push하여 release 브랜치를 공유합니다.

1. release-1.0.0 브랜치를 생성합니다.
   (develop)]$ git fetch upstream
   (develop)]$ git checkout -b release-1.0.0 –track upstream/develop

2. release-1.0.0 브랜치를 upstream에 push합니다.
   (release-1.0.0)]$ git push upstream release-1.0.0

## QA 중 버그 수정하기

개발을 완료한 후 QA 중 버그가 발생하지 않으면 좋겠지만 항상 생각지 못한 예외 상황들이 발생하게 됩니다. 예외 상황이 발생할 때마다 버그 티켓이 하나씩 생성되는데 이 티켓들을 모두 해결해야만 앱을 출시할 수 있습니다.
버그 티켓들도 티켓이기 때문에 ‘1. 티켓 처리하기’와 같은 방법으로 처리합니다.

1. release 브랜치에서 버그 티켓에 대한 브랜치를 생성합니다.
   (release-1.0.0)]$ git checkout -b bfm-101_bug_login_id_max_length

2. 버그를 수정합니다. (뚝딱뚝딱 :hammer:)
3. 작업 브랜치에 버그 수정 사항을 커밋합니다.
   (bfm-101_bug_login_id_max_length)]$ git commit -m "BFM-101 로그인 아이디 길이 제한 버그 수정"

4. 작업 브랜치를 origin에 push 합니다.
   (bfm-101_bug_login_id_max_length)]$ git push origin bfm-101_bug_login_id_max_length

5. Github에서 bfm-101_bug_login_id_max_length 브랜치를 release-1.0.0에 merge 하는 Pull Request를 생성합니다.
6. 동료에게 리뷰 승인을 받은 후 자신의 Pull Request를 merge 합니다.

## 앱 출시

발생하는 버그들을 모두 수정했다면 이젠 출시를 준비할 때입니다. release 브랜치를 master 브랜치와 develop 브랜치에 merge하고 마지막으로 master 브랜치에서 버전 태그를 달아줍니다.

1. release 브랜치를 최신 상태로 갱신합니다.
   (release-1.0.0)]$ git pull upstream release-1.0.0

2. release 브랜치를 develop 브랜치에 merge 합니다.
   (release-1.0.0)]$ git checkout develop
   (develop)]$ git pull upstream develop
   (develop)]$ git merge –no-ff release-1.0.0

3. develop 브랜치를 upstream에 push 합니다.
   (develop)]$ git push upstream develop

4. release 브랜치를 master 브랜치에 merge 합니다.
   (develop)]$ git checkout master
   (master)]$ git pull upstream master
   (master)]$ git merge –no-ff release-1.0.0

5. 1.0.0 태그를 추가합니다.
   (master)]$ git tag 1.0.0

6. master 브랜치와 1.0.0 태그를 upstream에 push 합니다.
   (master)]$ git push upstream master 1.0.0
