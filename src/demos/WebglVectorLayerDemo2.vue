<template>
  <form>
    <fieldset>
      <label for="timestamp">Current time shown</label>
      <input type="range" id="timestamp" min="1303200000" max="1303240000" v-model.number="timestamp" />
      <span class="description">{{ new Date(timestamp * 1000).toUTCString() }}</span>
    </fieldset>
  </form>

  <ol-map :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height: 400px">
    <ol-view ref="view" :center="center" :zoom="zoom" :projection="projection" />

    <ol-tile-layer>
      <ol-source-osm crossOrigin="anonymous" />
    </ol-tile-layer>

    <!-- webgl lines layer -->
    <ol-webgl-vector-layer :styles="webglLineStyle" :variables="webglVariables">
      <ol-source-vector ref="sourceRef" />
    </ol-webgl-vector-layer>

  </ol-map>
</template>

<script setup lang="ts">
import { computed, inject, onMounted, ref } from "vue";

const sourceRef = ref();

const timestamp = ref(1303240000);
const center = ref([703365.7089403362, 5714629.865071137]);
const projection = ref("EPSG:3857");
const zoom = ref(9);

const format = inject("ol-format");
const igc = new format.IGC();

const igcUrls = [
  'https://openlayers.org/en/latest/examples/data/igc/Clement-Latour.igc',
  'https://openlayers.org/en/latest/examples/data/igc/Damien-de-Baenst.igc',
  'https://openlayers.org/en/latest/examples/data/igc/Sylvain-Dhonneur.igc',
  'https://openlayers.org/en/latest/examples/data/igc/Tom-Payne.igc',
  'https://openlayers.org/en/latest/examples/data/igc/Ulrich-Prinz.igc',
];

onMounted(() => {
  for (let i = 0; i < igcUrls.length; ++i) {
    fetch(igcUrls[i])
      .then((resp) => resp.text())
      .then((data) => {
        const features = igc.readFeatures(data, {
          featureProjection: 'EPSG:3857',
        });
        sourceRef.value.source.addFeatures(features);
      });
  }
})

const webglLineStyle = {
  filter: ['<=', ['line-metric'], ['var', 'timestamp']],
  style: {
    'stroke-width': 4,
    'stroke-color': [
      'interpolate',
      ['linear'],
      ['line-metric'],
      1303200000,
      'hsl(312,100%,39%)',
      1303240000,
      'hsl(36,100%,45%)',
    ],
  }
};

const webglVariables = computed(() => ({
  timestamp: timestamp.value,
}));

</script>
