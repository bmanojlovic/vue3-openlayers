<template>
  <slot></slot>
</template>

<script setup lang="ts">
import { inject, onMounted, onUnmounted, computed, watch, nextTick } from "vue";
import Synchronize, { type Options } from "ol-ext/interaction/Synchronize";
import type Map from "ol/Map";
import usePropsAsObjectProperties from "@/composables/usePropsAsObjectProperties";

defineOptions({
  inheritAttrs: false,
});

const props = withDefaults(defineProps<Options>(), {
  maps: () => [],
});

const map = inject<Map>("map");
const properties = usePropsAsObjectProperties(props);

const synchronize = computed(
  () =>
    new Synchronize({
      ...properties,
    }),
);

watch(
  synchronize,
  async (newVal, oldVal) => {
    if (oldVal) map?.removeInteraction(oldVal);
    await nextTick();
    if (map?.getTargetElement()) {
      map.addInteraction(newVal);
      map.changed();
    }
  },
  { immediate: false }
);

onMounted(async () => {
  await nextTick();
  if (map?.getTargetElement()) {
    map.addInteraction(synchronize.value);
  }
});

onUnmounted(() => {
  map?.removeInteraction(synchronize.value);
});

defineExpose({
  synchronize,
});
</script>
