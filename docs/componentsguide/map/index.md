# ol-map

> The core component of vue3-openlayers

This is the main container for all other vue3-openlayers components and has one `default`
slot to place them all. Usually you will use it together with `ol-view`
component to setup `zoom`, `center`, `projection` and other view related properties for the map.

[[toc]]

## Setup

<!--@include: ../map.plugin.md-->

## Usage

<script setup lang="ts">
import ViewDemo from "@demos/ViewDemo.vue";
import ExistingMapDemo from "@demos/ExistingMapDemo.vue";
</script>

| Plugin Usage | Explicit Import |
| ------------ | :-------------: |
| `<ol-map>`   |  `<Map.OlMap>`  |

Example of a simple map.
See also documentation of `ol-view` component.

<ClientOnly>

<ViewDemo />
</ClientOnly>

::: code-group

<<< ../../../src/demos/ViewDemo.vue

:::

### re-use existing map

<ClientOnly>
<ExistingMapDemo />
</ClientOnly>

::: code-group

<<< ../../../src/demos/ExistingMapDemo.vue

:::

## Properties

### Props from OpenLayers

Properties are passed-trough from OpenLayers directly.
Their types and default values can be checked-out [in the official OpenLayers docs](https://openlayers.org/en/latest/apidoc/module-ol_Map-Map.html).
Only some properties deviate caused by reserved keywords from Vue / HTML.
This deviating props are described in the section below.

### Deviating Properties

#### instance

You can re-use an existing [OpenLayers `Map`](https://openlayers.org/en/latest/apidoc/module-ol_Map-Map.html) instance.
This is probably useful if your app already includes OpenLayers or some other library which uses OpenLayers and exposes its instance.
The passed `instance` property must be a valid instance of `ol/Map`.

## Events

You have access to all Events from the underlying source.
Check out [the official OpenLayers docs](https://openlayers.org/en/latest/apidoc/module-ol_Map-Map.html) to see the available events tht will be fired.

```html
<ol-map @error="handleEvent">
  <!-- ... -->
</ol-map>
```

## Methods

You have access to all Methods from the underlying source.
Check out [the official OpenLayers docs](https://openlayers.org/en/latest/apidoc/module-ol_Map-Map.html) to see the available methods.

To access the source, you can use a `ref()` as shown below:

```vue
<template>
  <!-- ... -->
  <ol-map ref="mapRef" @error="handleEvent">
    <!-- ... -->
  </ol-map>
  <!-- ... -->
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import type Map from "ol/Map";

const mapRef = ref<{ map: Map }>(null);

onMounted(() => {
  const map: Map = mapRef.value?.map;
  // call your method on `map`
});
</script>
```

## Show loading state

When layers are loaded, you can show a loading indicator by styling the `ol-map-loading` class.
