# framer motion

Motion은 Framer 의 React용 프로덕션 준비 모션 라이브러리입니다 . HTML 및 SVG 의미 체계를 유지하면서 선언적 애니메이션, 손쉬운 레이아웃 전환 및 제스처를 제공합니다.

Motion은 강력한 제스처 인식기로 React의 이벤트 시스템을 확장합니다. 호버, 탭, 팬 및 드래그를 지원합니다.

```jsx
<motion.div drag="x" dragConstraints={{ left: -100, right: 100 }} />
```

animate변형을 사용하여 단일 소품 으로 구성 요소의 전체 하위 트리를 애니메이션할 수 있습니다 . when및 같은 옵션 staggerChildren을 사용하여 이러한 애니메이션을 선언적으로 조정할 수 있습니다.

```jsx
const list = { hidden: { opacity: 0 } };
const item = { hidden: { x: -10, opacity: 0 } };

return (
  <motion.ul animate="hidden" variants={list}>
    <motion.li variants={item} />
    <motion.li variants={item} />
    <motion.li variants={item} />
  </motion.ul>
);
```

MotionValue애니메이션 및/또는 제스처의 결과로 업데이트할 수 있는 선언적 반응 체인을 만듭니다 .

```jsx
const x = useMotionValue(0);
const opacity = useTransform(x, [-100, 0, 100], [0, 1, 0]);

return <motion.div drag="x" style={{ x, opacity }} />;
```

MotionValue애니메이션 및/또는 제스처의 결과로 업데이트할 수 있는 선언적 반응 체인을 만듭니다 .

```jsx
const { scrollYProgress } = useViewportScroll();

return <motion.path style={{ pathLength: scrollYProgress }} />;
```
