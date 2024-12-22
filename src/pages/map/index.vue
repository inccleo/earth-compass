<template>
  <div class="map-container">
    <vc-viewer
      :animation="false"
      :timeline="false"
      @ready="onViewerReady"
    >
      <!-- 添加影像图层 -->
      <vc-layer-imagery>
        <vc-imagery-provider-arcgis
          :url="'https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer'"
        />
      </vc-layer-imagery>
    </vc-viewer>
  </div>
</template>

<script setup lang="ts">

const onViewerReady = (readyObj: any) => {
  // readyObj 包含 Cesium、viewer 等对象
  const { Cesium, viewer } = readyObj

  // 设置默认视角
  viewer.camera.setView({
    destination: Cesium.Cartesian3.fromDegrees(
      // 深圳
      114.06, 22.54,
      // 高度
      1000
    )
  })
  // 隐藏 版权
  viewer._cesiumWidget._creditContainer.style.display = "none";

}
</script>

<style scoped>
.map-container {
  width: 100%;
  height: 100vh;
}
</style>

<route lang="json5">
{
  name: 'map',
  meta: {
    title: '地图',
    i18n: 'menus.map'
  },
}
</route>
