---
sidebar_position: 2
---

# 核心概念

## 场景(Scene)

> 场景能够让你在什么地方、摆放什么东西来交给 three.js 来渲染，这是你放置物体、灯光和摄像机的地方。

### 三维物体（Object3D）

> 这是 Three.js 中大部分对象的基类，提供了一系列的属性和方法来对三维空间中的物体进行操纵。

```ts
import * as THREE from 'three'

const geometry = new THREE.BoxGeometry(1, 1, 1) // 几何体(正方体)
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 }) // 材质
const cube = new THREE.Mesh(geometry, material) // 网格（Mesh）表示基于以三角形为polygon mesh（多边形网格）的物体的类。 同时也作为其他类的基类

const scene = new THREE.Scene()
// scene.add 将 三维物体添加到场景中 进行渲染
scene.add(cube)
```

## 相机(Camera)

### PerspectiveCamera（透视摄像机）

> 这一摄像机使用 perspective projection（透视投影）来进行投影。这一投影模式被用来模拟人眼所看到的景象，它是 3D 场景的渲染中使用得最普遍的投影模式。

> 在大多数属性发生改变之后，你将需要调用.updateProjectionMatrix 来使得这些改变生效。

#### 参数

```ts
// PerspectiveCamera( fov : Number, aspect : Number, near : Number, far : Number )
// fov — 摄像机视锥体垂直视野角度 默认 50
// aspect — 摄像机视锥体长宽比 默认 1
// near — 摄像机视锥体近端面  默认 0.1
// far — 摄像机视锥体远端面  默认 2000
const camera = new THREE.PerspectiveCamera(45, width / height, 1, 1000)
scene.add(camera)
```

## 渲染器(Renderer)

> WebGL Render 用 WebGL 渲染出你精心制作的场景,常用 `WebGLRenderer` ,其他渲染器根据场景进行选择.

### WebGLRenderer

```ts
import * as THREE from 'three'

// 参数
const parameters : WebGLRendererParameters {
//   canvas: document.querySelector('canvas'),    // canvas - 一个供渲染器绘制其输出的canvas 它和下面的domElement属性对应。 如果没有传这个参数，会创建一个新canvas
    //...
}

const renderer = new THREE.WebGLRenderer(parameters)
 renderer.setSize(window.innerWidth, window.innerHeight) // 如果未知设置canvas参数,用setSize调整渲染大小

// 属性
renderer.domElement //一个canvas，渲染器在其上绘制输出。
// 渲染器的构造函数会自动创建(如果没有传入canvas参数);你需要做的仅仅是像下面这样将它加页面里去:
document.body.appendChild( renderer.domElement );
```

### 动画渲染

```ts
function animate() {
  requestAnimationFrame(animate) // requestAnimationFrame 执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。
  // 修改属性,重新渲染
  renderer.render(scene, camera)
}

animate()
```
