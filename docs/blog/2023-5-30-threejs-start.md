---
slug: threejs-start
title: three.js 轻松入门
authors: joey
tags: [three.js]
---

[three.js](https://threejs.org/)是一个开源的，功能齐全的 3D WebGL 库，在 web 3D 渲染中得到广泛应用，让我们一起进入 three.js 3D 世界吧。

<!--truncate-->

## 安装

推荐使用 npm 等包管理工具安装，因为可以一起安装 three.js 核心库和一些实用的插件。

```sh
npm install three
```

使用 CDN 导入参考官方文档 [安装 – three.js docs (threejs.org)](https://threejs.org/docs/index.html#manual/zh/introduction/Installation)

## 三要素

- 场景（Scene）
- 相机（Camera）
- 渲染器（Renderer）

### 场景（Scene）

```js
import * as THREE from 'three'

const scene = new THREE.Scene()
```

现在已经创建了一个 `Scene`，当然没有实际意义，因为 `Scene`中没有任何 3D 对象，我们可以使用 `scene.add()`将 3D 对象添加到`Scene`中。

```js
const geometry = new THREE.BoxGeometry(1, 1, 1) // 创建几何体
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 }) // 基础网格材质 颜色绿色
const cube = new THREE.Mesh(geometry, material) // 3D对象（网格）
scene.add(cube) // 将 3D对象 添加到 scene 中
```

#### 加载 3D 模型

加载 3D 模型也是工作中常见的需求

```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js' // 加载器

const loader = new GLTFLoader()

loader.load(
  'path/to/model.glb',
  function (gltf) {
    scene.add(gltf.scene) // 模型添加到 scene 中
  },
  undefined,
  function (error) {
    console.error(error)
  }
)
```

### 相机（Camera）

透视相机（PerspectiveCamera），这一投影模式被用来模拟人眼所看到的景象，它是 3D 场景的渲染中使用得最普遍的投影模式。

```js
const camera = new THREE.PerspectiveCamera(
  45,
  window.innerWidth / window.innerHeight,
  1,
  1000
) // 创建透视相机
//PerspectiveCamera( fov : Number, aspect : Number, near : Number, far : Number )
// fov — 视角（摄像机视锥体垂直视野角度） 默认 50
// aspect — 渲染视图长宽比 一般为渲染的canvas的长宽比
// near — 视线的最近点，渲染出来的画面如果最近处的画面被裁，可以调整此参数 默认 0.1
// far — 视线的最远点，渲染出来的画面如果最远处的画面被裁，可以调整此参数 默认 2000
scene.add(camera) // 将 相机 添加到 scene 中
```

### 渲染器（Renderer）

```js
const renderer = new THREE.WebGLRenderer() // 创建渲染器
renderer.setSize(window.innerWidth, window.innerHeight) // 设置渲染器尺寸
document.body.appendChild(renderer.domElement) // body 添加渲染器 DOM 元素

renderer.render( scene, camera ) // 三要素结合，将 3D 对象渲染到浏览器
```

#### 动画渲染

修改 3D 对象、相机等的某些参数，然后使用 `requestAnimationFrame` 每帧进行渲染，可以实现动画效果。

```js
function animate() {
  requestAnimationFrame(animate)

  cube.rotation.x += 0.01
  cube.rotation.y += 0.01

  renderer.render(scene, camera)
}

animate()
```

### 预览

![three-start.jpg](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6c8ffb0b8dbb447589b99b2dffb1c41b~tplv-k3u1fbpfcp-watermark.image?)

