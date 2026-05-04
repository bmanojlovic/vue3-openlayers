<template>
  <div>
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
import { provide, watch } from "vue";
import useLayer from "@/composables/useLayer";
import { type LayersCommonProps } from "@/components/layers/LayersCommonProps";
import WebGLVectorLayer, { type Options } from "ol/layer/WebGLVector";
import type { LayerEvents } from "@/composables";
import { useDefaults } from "@/components/layers/LayersCommonProps";
import type { LayerSwitcherOptions } from "@/types";


type Props = Omit<Options, "style"> & LayersCommonProps & LayerSwitcherOptions & {
  styles?: Options["style"];
};
const props = withDefaults(defineProps<Props>(), useDefaults<Props>({
  styles: () => ({
    "shape-points": 1,
    "shape-radius": 10,
    "shape-opacity": 0.5,
    "shape-fill-color": "blue",
  }),
}));

defineEmits<LayerEvents>();

const { layer } = useLayer(WebGLVectorLayer, props);

provide("webglVectorLayer", layer);

watch(
  () => props.variables,
  (newVariables) => {
    if (newVariables) {
      layer.value.updateStyleVariables(newVariables);
    }
  },
);

defineExpose({
  webglVectorLayer: layer,
});
</script>
