---
sidebar_position: 1
---

# 起步

## 安装

> https://threejs.org/docs/index.html#manual/zh/introduction/Installation

## [创建场景](https://threejs.org/docs/index.html#manual/zh/introduction/Creating-a-scene)

### 三要素

- [renderer（渲染器)](https://threejs.org/docs/index.html#api/zh/renderers/WebGLRenderer)
- [scene（场景）](https://threejs.org/docs/index.html#api/zh/scenes/Scene)
- [camera（相机）](https://threejs.org/docs/index.html#api/zh/cameras/Camera)

```html
<html>
  <head>
    <meta charset="utf-8" />
    <title>My first three.js app</title>
    <style>
      body {
        margin: 0;
      }
    </style>
  </head>
  <body>
    <script type="module">
      import * as THREE from 'https://unpkg.com/three/build/three.module.js'

      const scene = new THREE.Scene()
      /*
       * 创捷 PerspectiveCamera (透视摄像机)
       * @param fov(视野角度)   默认 50
       * @param aspect ratio(长宽比) 默认 1
       * @param near(近截面) 默认 0.1
       * @param far(远截面) 默认 2000
       */
      const camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      )
      /**
       * 渲染器  WebGL渲染器, 还有其他渲染器进行降级处理
       */
      const renderer = new THREE.WebGLRenderer()
      renderer.setSize(window.innerWidth, window.innerHeight)
      document.body.appendChild(renderer.domElement)

      /**
       * 立方体 参数为 长宽高
       */
      const geometry = new THREE.BoxGeometry(1, 1, 1)
      /**
       * 材质 参数有 颜色...
       */
      const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 })
      /**
       * Mesh（网格）网格包含一个几何体以及作用在此几何体上的材质
       */
      const cube = new THREE.Mesh(geometry, material)
      scene.add(cube)
      // 稍微向外移动摄像机
      camera.position.z = 5

      function animate() {
        requestAnimationFrame(animate)

        cube.rotation.x += 0.01
        cube.rotation.y += 0.01

        renderer.render(scene, camera)
      }

      animate()
    </script>
  </body>
</html>
```

```jsx live
function ThreeStart(props) {
  return (
    <>
      <a href="/three/start.html" target="_blank" rel="noopener noreferrer">
        全屏预览
      </a>
      <iframe
        style={{ width: '100%', height: '50vh' }}
        src="/three/start.html"
        frameBorder="0"
      ></iframe>
    </>
  )
}
```

## [画线（Drawing lines）](https://threejs.org/docs/index.html#manual/zh/introduction/Drawing-lines)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Drawing lines</title>
  </head>
  <style>
    body {
      margin: 0;
    }
  </style>

  <body></body>
  <script type="importmap">
    {
      "imports": {
        "three": "https://unpkg.com/three/build/three.module.js"
      }
    }
  </script>

  <script type="module">
    import * as THREE from 'three'
    // 渲染器
    const renderer = new THREE.WebGLRenderer()
    renderer.setSize(window.innerWidth, window.innerHeight)
    document.body.appendChild(renderer.domElement)
    // 相机
    const camera = new THREE.PerspectiveCamera(
      45,
      window.innerWidth / window.innerHeight,
      1,
      500
    )
    camera.position.set(0, 0, 100)
    camera.lookAt(0, 0, 0)

    // 场景
    const scene = new THREE.Scene()
    // 线条材质
    const material = new THREE.LineBasicMaterial({ color: 0x0000ff })

    const points = []
    points.push(new THREE.Vector3(-10, 0, 0))
    points.push(new THREE.Vector3(0, 10, 0))
    points.push(new THREE.Vector3(10, 0, 0))

    // 几何体
    const geometry = new THREE.BufferGeometry().setFromPoints(points)
    // 线条
    const line = new THREE.Line(geometry, material)
    // 添加到场景中
    scene.add(line)
    // 渲染
    renderer.render(scene, camera)
  </script>
</html>
```

```jsx live
function ThreeLine(props) {
  return (
    <>
      <a href="/three/line.html" target="_blank" rel="noopener noreferrer">
        全屏预览
      </a>
      <iframe
        style={{ width: '100%', height: '50vh' }}
        src="/three/line.html"
        frameBorder="0"
      ></iframe>
    </>
  )
}
```
