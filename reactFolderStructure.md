# react folder structure

## 디렉터리 구조

최상위 디렉토리 구조는 다음과 같습니다

- assets - 이미지, svgs, 회사 로고 등과 같은 글로벌 정적 자산
- components - 레이아웃(래퍼, 탐색), 양식 구성 요소, 버튼과 같은 전역 공유/재사용 가능한 구성 요소 navigation)
- services - JavaScript 모듈
- store - 글로벌 Redux 스토어
- utils - U유틸리티, 도우미, 상수 등
- views - "페이지"라고도 하며 대부분의 앱이 여기에 포함됩니다.

```txt
.
└── /src
    ├── /assets
    ├── /components
    ├── /services
    ├── /store
    ├── /utils
    ├── /views
    ├── index.js
    └── App.js
```

몇 가지 추가 폴더 볼 수 있다. types는, 타이프 프로젝트의 경우 middleware필요한 경우 아마도 context에 대한 컨텍스트 등

## 별칭

내에서 아무것도 그래서 나는 별칭을 사용하도록 시스템을 설정합니다 components폴더로 가져올 수있는 @components, assets같은 @assets사용자 정의 웹팩는, 이것이 통해 수행되는 경우 등, 해결의 구성.

```txt
module.exports = {
  resolve: {
    extensions: ['js', 'ts'],
    alias: {
      '@': path.resolve(__dirname, 'src'),
      '@assets': path.resolve(__dirname, 'src/components'),
      '@components': path.resolve(__dirname, 'src/components'),
      // ...etc
    },
  },
}
```

프로젝트 내 어디에서나 가져오기를 훨씬 쉽게 만들고 가져오기를 변경하지 않고 파일을 이동할 수 있으며

## components

components폴더 내에서 유형별로 그룹화합니다 forms. tables, buttons, layout, 등. 세부 사항은 특정 앱에 따라 다릅니다.

이 예에서는 고유한 양식 시스템을 생성하거나 기존 양식 시스템에 대한 고유한 바인딩을 생성한다고 가정합니다(예: Formik 및 Material UI 결합). 이 경우 각 구성 요소( TextField, Select, Radio, Dropdown등)에 대한 폴더를 만들고 내부에는 구성 요소 자체, 스타일, 테스트 및 사용 중인 경우 스토리북에 대한 파일이 있습니다.

- Component.js - 실제 React 구성 요소
- Component.styles.js - 구성 요소에 대한 스타일이 지정된 구성 요소 파일
- Component.test.js - 테스트
- Component.stories.js - 스토리북 파일

이것은 모든 구성 요소에 대한 파일이 포함된 폴더 하나, 모든 테스트가 포함된 폴더 하나, 모든 스토리북 파일이 포함된 폴더 하나 등을 갖는 것보다 훨씬 더 의미가 있습니다. 관련된 모든 것이 함께 그룹화되어 쉽게 찾을 수 있습니다.

```txt
.
└── /src
    └── /components
        ├── /forms
        │   ├── /TextField
        │   │   ├── TextField.js
        │   │   ├── TextField.styles.js
        │   │   ├── TextField.test.js
        │   │   └── TextField.stories.js
        │   ├── /Select
        │   │   ├── Select.js
        │   │   ├── Select.styles.js
        │   │   ├── Select.test.js
        │   │   └── Select.stories.js
        │   └── index.js
        ├── /routing
        │   └── /PrivateRoute
        │       ├── /PrivateRoute.js
        │       └── /PrivateRoute.test.js
        └── /layout
            └── /navigation
                └── /NavBar
                    ├── NavBar.js
                    ├── NavBar.styles.js
                    ├── NavBar.test.js
                    └── NavBar.stories.js
```

## service

응용 프로그램의 나머지가 사용하고있는 일반 자바 스크립트 모듈을 제작하는 경우, 그것은 편리 할 수 있습니다. 일반적으로 고안된 예는 다음과 같은 LocalStorage 모듈입니다.

```txt
.
└── /src
    └── /services
        ├── /LocalStorage
        │   ├── LocalStorage.service.js
        │   └── LocalStorage.test.js
        └── index.js
```

```js
export const LocalStorage = {
  get(key) {},
  set(key, value) {},
  remove(key) {},
  clear() {},
};
import { LocalStorage } from "@services";

LocalStorage.get("foo");
```

## store

전역 데이터 저장소는 store디렉터리(이 경우 Redux)에 포함됩니다. 각 기능에는 Redux Toolkit 슬라이스와 작업 및 테스트 가 포함될 폴더가 있습니다 . 이 설정은 또한 정기적으로 돌아 오는 사용할 수 있습니다, 당신은 단지 만들 것 .reducers.js파일 .actions.js대신의 파일을 slice. sagas를 사용하는 경우 Redux Thunk 작업 .saga.js대신 사용할 수 있습니다 .actions.js.

```txt
.
└── /src
    ├── /store
    │   ├── /authentication
    │   │   ├── /authentication.slice.js
    │   │   ├── /authentication.actions.js
    │   │   └── /authentication.test.js
    │   ├── /authors
    │   │   ├── /authors.slice.js
    │   │   ├── /authors.actions.js
    │   │   └── /authors.test.js
    │   └── /books
    │       ├── /books.slice.js
    │       ├── /books.actions.js
    │       └── /books.test.js
    ├── rootReducer.js
    └── index.js
```

## util

프로젝트에 utils폴더가 필요한지 여부 는 사용자에게 달려 있지만 일반적으로 앱의 여러 섹션에서 쉽게 사용할 수 있는 유효성 검사 및 변환과 같은 일부 전역 유틸리티 기능이 있다고 생각합니다. helpers.js수천 개의 기능을 포함 하는 하나의 파일이 아니라 정리를 유지하면 프로젝트 구성에 도움이 될 수 있습니다.

```txt
.
└── src
    └── /utils
        ├── /constants
        │   └── countries.constants.js
        └── /helpers
            ├── validation.helpers.js
            ├── currency.helpers.js
            └── array.helpers.js
```

다시 말하지만, utils폴더에는 글로벌 수준으로 유지하는 것이 합리적이라고 생각하는 모든 것이 포함될 수 있습니다. "다중 계층" 파일 이름을 선호하지 않으면 그냥 호출할 수 validation.js있지만 내가 보기에 명시적이라고 해서 프로젝트에서 아무 것도 가져갈 수 없으며 IDE에서 검색할 때 파일 이름을 더 쉽게 탐색할 수 있습니다.

## Views

다음은 앱의 주요 부분이 위치할 views디렉토리입니다. 앱의 모든 페이지는 "보기"입니다. 이 작은 예에서 보기는 Redux 스토어와 매우 잘 일치하지만 스토어와 보기가 정확히 같은 경우는 아니므로 별도의 것입니다. 또한 에서 books가져올 수 있습니다 authors.

보기 내의 모든 항목은 해당 특정 보기 내에서만 사용되는 항목입니다. 이 항목 BookForm은 /books경로 에서만 사용되며 경로 AuthorBlurb에서만 사용됩니다 /authors. 여기에는 특정 양식, 모달, 버튼, 전역적이지 않은 구성 요소가 포함될 수 있습니다.

모든 페이지를 한 components/pages곳에 모으는 대신 모든 것을 도메인 중심으로 유지하는 것의 장점은 애플리케이션의 구조를 보고 얼마나 많은 최상위 뷰가 있는지, 해당 애플리케이션에서만 사용되는 모든 것이 어디에 있는지 알기가 정말 쉽다는 것입니다. 보기는. 중첩된 경로가 views있는 경우 기본 경로 내에 항상 중첩된 폴더를 추가할 수 있습니다 .

```txt
.
└── /src
    └── /views
        ├── /Authors
        │   ├── /AuthorsPage
        │   │   ├── AuthorsPage.js
        │   │   └── AuthorsPage.test.js
        │   └── /AuthorBlurb
        │       ├── /AuthorBlurb.js
        │       └── /AuthorBlurb.test.js
        ├── /Books
        │   ├── /BooksPage
        │   │   ├── BooksPage.js
        │   │   └── BooksPage.test.js
        │   └── /BookForm
        │       ├── /BookForm.js
        │       └── /BookForm.test.js
        └── /Login
            ├── LoginPage
            │   ├── LoginPage.styles.js
            │   ├── LoginPage.js
            │   └── LoginPage.test.js
            └── LoginForm
                ├── LoginForm.js
                └── LoginForm.test.js
```

## api

api디렉토리는 응용 프로그램 (프론트 엔드)와 API (백엔드) 반작용 사이의 통신을 돌봐 모든 서비스가 포함되어 있습니다. 단일 서비스는 HTTP 프로토콜을 사용하여 외부 서비스에서 데이터를 검색하거나 외부 서비스에 데이터를 게시하는 여러 기능을 제공합니다.

auth.js인증을 위한 기능을 제공 하고 발신 HTTP 요청 및 수신 응답에 대한 인터셉터를 axios.js포함하는 axios 인스턴스를 포함합니다. 또한 JWT를 새로 고치는 프로세스가 여기에서 처리됩니다.

```txt
├── api
│   ├── services
│   │   ├── Job.js
│   │   ├── User.js
│   ├── auth.js
│   └── axios.js
```
