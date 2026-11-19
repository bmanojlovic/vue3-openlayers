<template>
  <div v-if="false"></div>
</template>
<script setup lang="ts">
import Profile from "ol-ext/control/Profile";
import type { Options as ControlOptions } from "ol/control/Control";
import type Feature from "ol/Feature";
import type { Style } from "ol/style";
import { useAttrs } from "vue";
import useControl from "@/composables/useControl";
import usePropsAsObjectProperties from "@/composables/usePropsAsObjectProperties";
import {
  useOpenLayersEvents,
  type CommonEvents,
} from "@/composables/useOpenLayersEvents";

// prevent warnings caused by event pass-through via useOpenLayersEvents composable
defineOptions({
  inheritAttrs: false,
});

// Options of ol-ext/control/Profile, declared here: @types/ol-ext 3.6.7 gives
// the Profile class a `static prototype` member, which the Vue SFC compiler
// (Babel) rejects while resolving an imported props type from that file.
interface Options extends ControlOptions {
  className?: string;
  title?: string;
  style?: Style;
  selectStyle?: Style;
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  info?: { [key: string]: any };
  width?: number;
  height?: number;
  units: "metric" | "imperial";
  feature?: Feature;
  selectable?: boolean;
  zoomable?: boolean;
  numberFormat?: string;
  skipFirst?: number;
}

const props = defineProps<Options>();
// Missing typings for events, use any
/* eslint-disable @typescript-eslint/no-explicit-any */
type Emits = CommonEvents & {
  (e: "over", ...args: any[]): void;
  (e: "out", ...args: any[]): void;
  (e: "show", ...args: any[]): void;
  (e: "dragstart", ...args: any[]): void;
  (e: "dragging", ...args: any[]): void;
  (e: "dragend", ...args: any[]): void;
  (e: "dragcancel", ...args: any[]): void;
};
/* eslint-enable @typescript-eslint/no-explicit-any */
defineEmits<Emits>();

const attrs = useAttrs();
const properties = usePropsAsObjectProperties(props);
const { control } = useControl(Profile, properties, attrs);

useOpenLayersEvents(control, [
  "over",
  "out",
  "show",
  "dragstart",
  "dragging",
  "dragend",
  "dragcancel",
]);

defineExpose({
  control,
});
</script>
