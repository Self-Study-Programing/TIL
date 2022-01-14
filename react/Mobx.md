# MobX

MobX는 전역 상태 라이브러리입니다. 모든 상태변화롤 일어나는 부분으로 자동으로 추적해주는 역할을 합니다.
상태관리는 왜 필요할까요? 첫번째로 유지보수가 쉬워지도록 상태 로직을 분리하여 모듈화 할 수 있고 두번째로 상태관리의 단계를 간결하게 해 줍니다.
MobX는 간단하고 확장 가능한 상태 관리 라이브러리를 철학으로 하고 있습니다.

MobX는 다음과 같은 특징을 가지고 있습니다.

- React에 종속적인 라이브러리가 아님
- 아키텍처나 상태 컨테이너가 아닌 라이브러리
- redux와 다르게 store에 제한이 없음
- 또한 redux에서 해줘야했던 action 선언, connect, mapStateToProps, mapDispatchToProps등 번거로운 작업들은 데코레이터로 간단하게 대체
- observable을 기본적으로 사용하고 있음
- Mobx는 절대적으로 필요한 경우에만 state 변경
- Typescript를 기반으로 만들어짐

![이미지](https://jeffgukang.github.io/react-native-tutorial/docs/state-tutorial/mobx-tutorial/images/mobx-core-idea.png)

- State(Observable State) - 관찰 받고 있는 상태

  - 모델을 채우는 객체, 비객체, 원시, 참조의 그래프
  - 어플리케이션의 데이터 셀
  - 특정 부분이 바뀌면, MobX에서는 정확히 어떤 부분이 바뀌었는지 알 수 있음
  - 이 state의 변화는 reaction과 computations를 일으킴

- Derivation(Computed values) - 파생 값(연산된 값)

  - Observable State의 변화에 따른 값
  - 기존의 상태값과 다른 연산된 값에 기반하여 만들어질 수 있는 값
  - 특정값을 연산할 때에만 처리됨
  - 어플리케이션으로부터 자동으로 계산될 수 있는 모든 값
  - observable로부터 도출할 수 있음 값이 변경되면 자동으로 업데이트
  - 성능최적화를 위해 사용

- Reactions - 반응

  - Observable State의 변화에 따른 부가적인 변화
  - 값이 바뀜에 따라 해야 할 일을 정하는 것을 의미
  - 파생 값과 비슷하지만 값을 생성하지 않는 함수
  - 대체로 I/O 와 관련된 작업
  - 적당할 때 자동으로 DOM이 업데이트 되거나 네트워크 요청을 하도록 만듬
  - when, autorun, reaction

- Actions : 액션

  - Observable State가 사용자가 지정한 것을 포함한 모든 변경사항
  - 상태를 변경시키는 모든 것
  - MobX는 모든 사용자의 모든 사용자의 액션으로 발생하는 상태 변화들이 전부 자동으로 파생값(Derivation)과 리엑션(Reactions)으로 처리되도록 함
