<template>
  <div id="app"></div>
</template>

<script>
import * as THREE from "three";
import { onMounted, reactive } from "vue";
export default {
  setup() {
    const header = reactive({
      camera: null,
      scene: null,
      renderer: null,
      mesh: null,
    });
    const init = () => {
      /**
       * 创建场景对象Scene
       */
      var scene = new THREE.Scene();
      /**
       * 创建网格模型
       */
      // var geometry = new THREE.IcosahedronGeometry(50); // 正二十面体
      // var geometry = new THREE.DodecahedronGeometry(50); // 正十二面体
      // var geometry = new THREE.OctahedronGeometry(50); // 正八面体
      var geometry3 = new THREE.CylinderGeometry(50, 50, 100, 25); // 圆柱
      var geometry4 = new THREE.BoxGeometry(100, 100, 100); //创建一个立方体几何对象Geometry
      var geometry2 = new THREE.SphereGeometry(60, 40, 40); //创建一个球体几何对象 3个参数 球的大小、球的精度（类似于正多面体）
      // 材质效果(设置光源的颜色、景深)
      // 材质对象的属性 color wireframe opacity transparent
      // 光的反射效果 MeshLambertMaterial 漫反射
      // Lambert网格材质，与光照有反应，漫反射 MeshLambertMaterial
      var material5 = new THREE.MeshLambertMaterial({
        color: 0xff00ff,
        wireframe: true,
      });

      var material3 = new THREE.MeshLambertMaterial({
        color: 0xffff00,
        opacity: 0.25, // 如果transparent设置为false 透明度将会无效
        transparent: false,
        wireframe: true,
      });

      // 镜面反射 高光Phong材质,与光照有反应
      var material4 = new THREE.MeshPhongMaterial({
        color: 0xffffff, // 材质颜色
        specular: 0x4488ee, // 高光颜色
        shininess: 12, // 光的强度系数
      });

      // 参数解读 光的颜色、光源的强度默认为1 、光线的强度默认为0
      var material2 = new THREE.DirectionalLight(0xac6c25, 1, 0);
      material2.position.set(0, 1, 1); // 光源的向量

      var mesh = new THREE.Mesh(geometry4, material4); //网格模型对象Mesh
      var mesh2 = new THREE.Mesh(geometry2, material5);
      var mesh3 = new THREE.Mesh(geometry3, material3);
      mesh2.translateY(120);
      mesh3.position.set(300, 200, 0); // X Y Z坐标
      scene.add(mesh);
      scene.add(material2);
      scene.add(mesh3);
      scene.add(mesh2);
      /**
       * 光源设置
       */
      //点光源
      var point = new THREE.PointLight(0xffffff);
      point.position.set(400, 200, 300); //点光源位置
      scene.add(point); //点光源添加到场景中
      //全局环境光
      var ambient = new THREE.AmbientLight(0x444444);
      scene.add(ambient);
      /**
       * 相机设置
       */
      var width = window.innerWidth; //窗口宽度
      var height = window.innerHeight; //窗口高度
      var k = width / height; //窗口宽高比
      var s = 200; //三维场景显示范围控制系数，系数越大，显示的范围越大
      //创建相机对象
      var camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000);
      camera.position.set(200, 300, 200); //设置相机位置
      camera.lookAt(scene.position); //设置相机方向(指向的场景对象)

      // scene.add(axisHelper);
      /**
       * 创建渲染器对象
       */
      var renderer = new THREE.WebGLRenderer();
      renderer.setSize(width, height); //设置渲染区域尺寸
      renderer.setClearColor(0xb9d3ff, 1); //设置背景颜色
      document.body.appendChild(renderer.domElement); //body元素中插入canvas对象
      var To = new Date();
      //执行渲染操作   指定场景、相机作为参数
      function render() {
        var T1 = new Date();
        var t = T1 - To;
        To = T1;
        renderer.render(scene, camera); //执行渲染操作
        mesh3.rotateY(0.0009 * t); //每次绕y轴旋转0.01弧度
        mesh2.rotateY(0.0009 * t); //每次绕y轴旋转0.01弧度
        window.requestAnimationFrame(render); // 此方法不能与addEventListener同时使用、会造成冲突
      }
      render();
      // 鼠标控制物体可以移动
      //   const controls = new THREE.OrbitControls(camera, renderer.domElement); //创建控件对象
    };
    const onWindowSize = () => {
      let container = document.getElementById("app");
      (header.camera.aspect = container.clientWidth / container.clientHeight),
        header.camera.updateProjectionMatrix();
      header.renderer.setSize(container.clientWidth, container.clientHeight);
    };
    const animate = () => {
      requestAnimationFrame(animate());
      header.mesh.rotation.x += 0.01;
      header.mesh.rotation.y += 0.02;
      header.renderer.render(header.scene, header.camera);
    };
    onMounted(() => {
      init();
      animate();
      window.addEventListener("resize", onWindowSize());
    });
    return {
    };
  },
};
</script>

<style>
</style>