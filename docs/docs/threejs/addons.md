---
sidebar_position: 3
---

# 实用插件

## 轨道控制器（OrbitControls）

> Orbit controls（轨道控制器）可以使得相机围绕目标进行轨道运动。

```ts
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

const controls = new OrbitControls( camera, renderer.domElement );
// 手动修改相机参数后,调用controls.update()更新
// camera.position.set( 0, 20, 100 );
// controls.update();
//  未使用requestAnimationFrame 进行每帧刷新时,可以箭头 change 事件,进行刷新
// controls.addEventListener('change',()=>{
//   renderer.render(scene, camera)
// })
```

```jsx live
function ThreeOrbitControls(props) {
  return (
    <>
      <a href="/three/orbit-controls.html" target="_blank" rel="noopener noreferrer">
        全屏预览
      </a>
      <iframe
        style={{ width: '100%', height: '50vh' }}
        src="/three/orbit-controls.html"
        frameBorder="0"
      ></iframe>
    </>
  )
}
```

## 坐标轴(AxesHelper)

> 用于简单模拟3个坐标轴的对象.红色代表 X 轴. 绿色代表 Y 轴. 蓝色代表 Z 轴


```ts
const axesHelper = new THREE.AxesHelper(150);
scene.add(axesHelper);
```

```jsx live
function ThreeAxesHelper(props) {
  return (
    <>
      <a href="/three/axe-helper.html" target="_blank" rel="noopener noreferrer">
        全屏预览
      </a>
      <iframe
        style={{ width: '100%', height: '50vh' }}
        src="/three/axe-helper.html"
        frameBorder="0"
      ></iframe>
    </>
  )
}
```