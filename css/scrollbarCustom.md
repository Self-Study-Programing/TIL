# scroll bar Custom

흔히들 보는 웹브라우저 스크롤 바는 회색깔이다. 이는 스크롤바로 인해 색깔이 어울리지 않아 완성도를 떨어뜨릴 수 있다

그래서 브라우저에선 ::-webkit-scrollbar으로 스크롤바를 custom 할 수 가있다.

::-webkit-scrollbar 속성에는

- ::-webkit-scrollbar-track
- ::-webkit-scrollbar-thumb
- ::-webkit-scrollbar-button:start:decrement
- ::-webkit-scrollbar-button:end:increment
- ::-webkit-scrollbar-corner

다음과 같이 있다

지금부터 하나씩 알아보며 스크롤바 커스텀에 대해 알아보겠다

## ::-webkit-scrollbar -> 스트롤바 전체

이는 스크롤바 전체 부분으로 예시를 들면

```css
::-webkit-scrollbar {
  width: 5px;
}
```

## ::-webkit-scrollbar-track -> 스크롤바에서 움직이는 영역

```css
::-webkit-scrollbar-track {
  background: linear-gradient(#e66465, #9198e5);
  border-radius: 10px;
}
```

## ::-webkit-scrollbar-button:start:decrement, ::-webkit-scrollbar-button:end:increment -> 스크롤바 각 끝 부분

```css
::-webkit-scrollbar-button:start:decrement,
::-webkit-scrollbar-button:end:increment {
  display: block;
  height: 8px;
  background: linear-gradient(#e66465, #9198e5);
}
```

## ::-webkit-scrollbar-corner -> 좌우 스크롤바와 상하 스크롤바가 만나는 영역

```css
::-webkit-scrollbar-corner {
  background: linear-gradient(#e66465, #9198e5);
}
```
