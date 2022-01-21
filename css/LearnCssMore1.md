## accent-color

MDN에 따르면 이는 'CSS 속성은 일부 요소에서 생성된 사용자 인터페이스 컨트롤의 강조 색상을 설정 합니다.'라고 표기되어 있다.

쉽게 말해 강조 색상을 설정 한다는 건 radiobutton이나 checkbox 같은 것을 체크하면 기본적으로 브라우저에서 파란색으로 체크가 되는 것을 확인할 수 있다 그 외에도 progress나 input:range와 같이 모두 파란색이 적용되는 것을 확인 할 수 있다.

이 색깔을 바꾸는 역할을 accent-color가 하는 것이다

```html
<label for="">
  <input type="range" value="배진영" />
  배진영
</label>
```

```css
input {
  accent-color: #ffff00;
}
```

![img](./img/accentColor.png)

## align-content

justify-content 기본 축 내에서 개별 항목을 정렬 하는 방법과 유사하게 교차 축에 추가 공간이 있을 때 플렉스 컨테이너의 라인을 정렬하는 데 도움이 됩니다.

이 속성은 flexbox에 한 줄만 있는 경우에는 효과가 없습니다.

이 align-content 속성은 6가지 다른 값을 허용합니다.

- flex-start: 컨테이너의 시작 부분에 채워진 줄
- flex-end: 컨테이너 끝까지 채워진 줄
- center: 용기 중앙에 채워진 선
- space-between: 선이 고르게 분포됨; 첫 번째 줄은 컨테이너의 시작 부분에 있고 마지막 줄은 끝에 있습니다.
- space-around: 선 사이에 동일한 간격으로 균등하게 분포된 선
- stretch ( 기본값 ): 나머지 공간을 차지하도록 줄이 늘어납니다.

## align-self

align-self속성은 Flexible Box Layout 모듈 의 하위 속성입니다 .

align-items특정 플렉스 항목 의 값을 재정의할 수 있습니다.

이 align-self속성은 다음과 동일한 5개의 값을 허용합니다 align-items.

- flex-start: 항목의 교차 시작 여백 가장자리가 교차 시작 라인에 배치됩니다.
- flex-end: 아이템의 크로스 엔드 여백 가장자리가 크로스 엔드 라인에 배치됩니다.
- center: 항목이 교차 축의 중앙에 있습니다.
- baseline: 기준선이 정렬된 것처럼 항목이 정렬됩니다.
- stretch (기본값): 컨테이너를 채우기 위해 늘이기(여전히 최소 너비/최대 너비를 준수함)

## all

CSS 의 속성 은 텍스트 방향을 제어 하는 및 속성을 all제외하고 선택한 요소의 모든 속성을 재설정합니다

- initial: 선택한 요소의 모든 속성을 CSS 사양에 정의된 초기 값으로 재설정합니다.
- inherit: 선택한 요소는 일반적으로 상속할 수 없는 스타일을 포함하여 상위 요소의 모든 스타일을 상속합니다.
- unset: 선택한 요소는 상위 요소에서 전달된 상속 가능한 값을 상속합니다. 상속 가능한 값이 없으면 CSS 사양의 초기 값이 각 속성에 사용됩니다.

일부 속성에는 사양에 명시적으로 정의된 초기 값이 없고 대신 사용자 에이전트가 초기 값을 설정할 수 color있으며 font-family두 가지 예가 있습니다. all: initial;또는 가 적용 되면 all: unset;사용자 에이전트 기본값 initial이 이러한 속성의 값으로 사용됩니다.

all단일 선언 으로 모든 CSS 속성 의 값을 한 번에 제어할 수 있기 때문에 "약식" 속성으로 간주됩니다 . 그러나 대부분의 속기 속성과 달리 실용적인 "장기" 버전이 없으며 하위 속성도 없습니다.

```css
.tag {
  all: initial;
}
```

## appearance

이 appearance속성은 사용자의 운영 체제 테마를 기반으로 하는 플랫폼 네이티브 스타일을 사용하여 요소를 표시하는 데 사용됩니다.

속성은 다음 appearance두 가지 이유 중 하나로 사용됩니다.

1. 기본적으로 없는 요소에 플랫폼별 스타일 지정을 적용하려면
2. 기본적으로 포함하는 요소에 대한 플랫폼별 스타일 지정을 제거하려면

```css
/* CSS Basic User Interface Module Level 4 values */
appearance: none;
appearance: auto;
appearance: menulist-button;
appearance: textfield;

/* "Compat-auto" values, which have the same effect as 'auto' */
appearance: button;
appearance: searchfield;
appearance: textarea;
appearance: push-button;
appearance: slider-horizontal;
appearance: checkbox;
appearance: radio;
appearance: square-button;
appearance: menulist;
appearance: listbox;
appearance: meter;
appearance: progress-bar;

/* Partial list of available values in Gecko */
-moz-appearance: scrollbarbutton-up;
-moz-appearance: button-bevel;

/* Partial list of available values in WebKit/Blink (as well as Gecko and Edge) */
-webkit-appearance: media-mute-button;
-webkit-appearance: caret;

/* Global values */
appearance: inherit;
appearance: initial;
appearance: revert;
appearance: unset;
```

## aspect-ratio

CSS 속성 을 사용하면 상자의 및 상자가 비율로 자동 계산 aspect-ratio되는 비례 치수를 유지하는 상자를 만들 수 있습니다 . 약간 수학적인 표현이지만 이 속성에서 한 값을 다른 값으로 나눌 수 있으며 계산된 값은 상자가 해당 비율로 유지되도록 합니다. height width

즉, 이 속성은 요소의 크기를 일관되게 조정하는 데 도움이 되므로 요소의 비율이 커지거나 줄어들 때 동일하게 유지됩니다.

```css
.element {
  aspect-ratio: 2 / 1; /* ↔️ is double the ↕️ */
}

.element {
  aspect-ratio: 1 / 1; /* ⏹ a perfect square */
}
```

### aspect-ratio가 적용되지 않는 경우

1. width요소에서 및 둘 다 height선언된 경우
2. 콘텐츠가 비율을 벗어날 때
3. min-*및 max-*속성 에 "손실"될 때

## backdrop-filter

backdrop-filterCSS 의 속성 은 요소의 배경/배경에 필터 효과 ( grayscale, contrast, 등)를 적용하는 데 사용됩니다. blur필터 효과가 요소 의 내용 대신 배경 에만 적용된다는 점을 제외하면 속성 backdrop-filter과 동일한 효과를 가 집니다.filter
backdrop-filter속성을 사용하면 이 추가 "배경" 요소를 제거하고 배경에 직접 필터를 적용할 수 있습니다 .

필터에는 다음과 같은 종류가 있습니다

- blur() -> 흐리게 하기
- brightness() -> 밝기
- contrast() -> 대비를 조정
- drop-shadow() -> 그림자 효과를 적용
- grayscale() -> 이미지를 회색조
- hue-rotate() -> 색조
- invert() -> 색상 샘플을 반전
- opacity() -> 투명도
- saturate() -> 과포화하거나 흐리게
- sepia() -> 세피아로 변환하여 더 따뜻하고 노란색/갈색
- url() – (SVG 필터 적용용)

```css
.tag {
  backdrop-filter: grayscale(0.5) opacity(0.3);
}
```

## backface-visibility

backface-visibility속성은 3D 변환과 관련이 있습니다 . 3D 변환을 사용하면 요소를 회전하여 요소의 "앞면"이라고 생각하는 것이 더 이상 화면을 향하지 않도록 관리할 수 있습니다.

- visible (기본값) – 요소는 화면을 향하지 않을 때에도 항상 표시됩니다.
- hidden– 화면을 향하지 않을 때는 요소가 보이지 않습니다 .
- inherit – 속성은 상위 요소에서 값을 가져옵니다.
- initial– 속성을 기본값인 로 설정합니다 visible.

```css
.tag {
  backface-visibility: visible | hidden;
}
```

## background-attachment

CSS 의 background-attachment속성은 뷰포트를 기준으로 배경을 이동하는 방법을 지정합니다.

background-attachment기본 보기(브라우저 창)와 로컬 보기(위의 데모에서 볼 수 있음) 에 대해 이야기할 때 생각할 수 있는 두 가지 다른 보기가 있습니다.

scroll기본값입니다. 기본 보기와 함께 스크롤되지만 로컬 보기 내에서는 고정된 상태로 유지됩니다.

fixed상관없이 고정됩니다. 이것은 일종의 물리적 창과 같습니다. 창 주위를 이동하면 관점이 변경되지만 사물이 창 외부에 있는 위치는 변경되지 않습니다.

## background-blend-mode

background-blend-mode속성은 요소가 다음과 어떻게 혼합 background-image되어야 하는지 정의합니다 background-color.

- normal: 위와 같이 background-color는 background-image를 통해 번지지 않습니다.
- multiply: background-image와 background-color가 곱해지며 일반적으로 이전보다 더 어두운 이미지로 이어집니다.
- screen: 이미지와 색상이 모두 반전되고 곱해지고 다시 반전됩니다.
- overlay: 배경색과 배경색을 혼합하여 배경의 명암을 반영한다
- darken: 배경 이미지가 배경 색상보다 어두우면 이미지가 교체되고 그렇지 않으면 그대로 유지됩니다.
- lighten: 배경 이미지가 배경 색상보다 밝으면 이미지가 교체되고, 그렇지 않으면 그대로 유지됩니다.
- color-dodge: 배경색을 배경 이미지의 역수로 나눕니다. 이것은 화면 혼합 모드와 매우 유사합니다
- color-burn: 배경색이 반전되어 배경 이미지로 분할되어 다시 반전됩니다. 이것은 곱하기와 비슷합니다
- hard-light: 배경 이미지가 배경 색상보다 밝으면 결과가 여러 번이고 더 밝으면 결과가 화면입니다.
- soft-light: 최종 결과는 hard-light이미지에 확산된 스포트라이트를 놓은 것처럼 보이지만 비슷하지만 더 부드럽습니다.
- difference: 가장 밝은 색상에서 배경 이미지의 어두운 색상과 배경 색상을 뺀 결과입니다. 종종 이미지의 대비가 매우 높습니다.
- exclusion: 결과는 와 매우 유사 difference하지만 대비가 약간 낮습니다.
- hue: 결과는 배경 색상의 광도 및 채도와 결합된 배경 이미지의 색조입니다.
- saturation: 배경색의 색조와 명도를 혼합하면서 배경 이미지의 채도를 유지합니다.
- color: 배경 이미지의 색조와 채도, 배경색의 명도를 유지합니다. 이 예에서는 이미지가 회색이고 효과가 회색 레벨을 유지하기 때문에 얻을 수 있는 것은 큰 회색 얼룩뿐입니다.
- luminosity: 배경색의 채도와 색조를 사용하면서 상단 색상의 명도를 유지합니다.

```css
.tag {
  background-blend-mode: screen, difference, lighten;
}
```

## background-clip

background-clip 배경 이미지나 색상이 요소의 패딩이나 콘텐츠를 넘어 확장되는 정도를 제어할 수 있습니다.

- border-box기본값입니다. 이렇게 하면 배경이 요소 테두리의 바깥쪽 가장자리까지 확장될 수 있습니다.
- padding-box 요소 패딩의 바깥쪽 가장자리에서 배경을 자르고 테두리 안으로 확장되지 않도록 합니다.
- content-box콘텐츠 상자의 가장자리에서 배경을 자릅니다.
- inheritbackground-clip부모의 설정을 선택한 요소에 적용합니다 .

## background-position

background-position속성을 사용하면 컨테이너 내에서 배경 이미지(또는 그라디언트)를 이동할 수 있습니다.

기본값은 0 0입니다. 그러면 컨테이너의 왼쪽 상단에 배경 이미지가 배치됩니다.

## block-overflow

텍스트를 자르고 속성 block-overflow에 의해 설정된 줄 수 뒤에 줄임표 또는 사용자 지정 문자열을 삽입하여 더 많은 내용이 뒤따르는 것을 나타냅니다 max-lines.

```css
.module {
  block-overflow: [clip | ellipsis | ];
  max-lines: []; /* required by block-overflow */
}
```

- clip: 다음에 추가할 텍스트를 나타내기 위해 문자를 삽입하지 않습니다. 대신 내용이 잘리고 마지막 문자에서 잘립니다.
- ellipsis: 마지막 줄 끝에 줄임표(…)를 표시합니다. 유니코드 문자(U+2026)로 렌더링되어야 하지만 사용 중인 사용자 에이전트의 콘텐츠 언어 및 쓰기 모드에 따라 동등한 문자로 대체될 수 있습니다.
- [ string ]: 마지막 줄 끝에 사용자 정의 텍스트(예: "더 읽기 →")를 표시합니다. 사양에 따르면 문자열이 "터무니없이" 길면 User-Agent가 문자열을 줄임표로 바꿀 수 있습니다.

## block-size

block-size가로일 때 요소 의 높이 , 세로일 때 요소 의 너비 를 정의 하는 CSS 논리 속성 입니다 .writing-modewriting-mode

```css
.element {
  block-size: 700px;
  writing-mode: vertical-lr;
}
```

## border-boundary

border-boundary속성은 요소의 경계가 작동하는 방식에 영향을 주는 요소의 경계에 대한 제약 조건을 설정합니다.

```css
.element {
  border-boundary: none | parent | display;
}
```

현재 지원 안함

- none: 경계선에 경계선이 설정되어 있지 않습니다.
- parent: 요소의 영역과 상위 요소의 테두리 가장자리가 만나는 경계를 설정합니다.
- display: 요소의 영역과 뷰포트의 경계 가장자리가 만나는 경계를 설정합니다

## border-collapse

border-collapse속성은 table요소(또는 또는 를 통해 테이블처럼 작동하도록 만들어진 요소 display: table) 에 사용됩니다 display: inline-table. 두 가지 값이 있습니다.

- separate (기본값) – 모든 테이블 셀에 자체 테두리가 있고 해당 셀 사이에도 공간이 있을 수 있습니다.
- collapse – 표 셀 사이의 공백과 테두리가 모두 축소되어 테두리가 하나만 있고 셀 사이에 공백이 없습니다.

## border-inline

```css
.element {
  border-inline: 5px solid red;
  writing-mode: horizontal-tb;
}
```

## box-decoration-break

이 box-decoration-break속성을 사용하면 "깨진" 요소 조각에 상자 장식을 그리는 방법을 제어할 수 있습니다. 요소는 줄 끝, 열 위 또는 페이지 나누기에서 조각으로 나눌 수 있습니다.

```css
.module {
  box-decoration-break: clone;
}
```

- slice: 초기 값. 상자 장식은 요소 전체에 적용되며 요소 조각의 가장자리에서 깨집니다.
- clone: 조각이 깨지지 않은 개별 요소인 것처럼 요소의 각 조각에 장식이 적용됩니다. 테두리는 요소의 각 조각의 네 가장자리를 감싸고 배경은 각 조각에 대해 완전히 다시 그려집니다.
