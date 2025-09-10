<template>
  <div style="display: flex; gap: 10px;">
    <div style="width: 400px; height: 300px;">
      <ol-map ref="map1" :loadTilesWhileAnimating="true" style="height: 100%">
        <ol-view :center="center" :zoom="zoom" />
        <ol-tile-layer>
          <ol-source-osm />
        </ol-tile-layer>
        <ol-interaction-synchronize :maps="syncMaps1" />
      </ol-map>
    </div>

    <div style="width: 400px; height: 300px;">
      <ol-map ref="map2" :loadTilesWhileAnimating="true" style="height: 100%">
        <ol-view :center="center" :zoom="zoom" />
        <ol-tile-layer>
          <ol-source-xyz url="https://tile.openstreetmap.org/{z}/{x}/{y}.png" />
        </ol-tile-layer>
        <ol-interaction-synchronize :maps="syncMaps2" />
      </ol-map>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

const center = ref([2226389.8158654715, 5465442.183322753]);
const zoom = ref(6);

const map1 = ref();
const map2 = ref();

const syncMaps1 = computed(() => map2.value?.map ? [map2.value.map] : []);
const syncMaps2 = computed(() => map1.value?.map ? [map1.value.map] : []);
</script>
