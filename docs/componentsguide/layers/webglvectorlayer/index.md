# ol-webgl-vector-layer

> A layer for rendering points, lines and polygons using WebGL

Please note, that you can't use `ol-style` and related style components here as child components.
For more information please checkout the [`ol-source-vector` docs](../../sources/vector/) as well.

[[toc]]

## Setup

<!--@include: ../../layers.plugin.md-->

## Usage

| Plugin Usage              |        Explicit Import        |
| ------------------------- | :---------------------------: |
| `<ol-webgl-vector-layer>` | `<Layers.OlWebglVectorLayer>` |

### WebGL Points, Lines, Polygons

<script setup lang="ts">
import WebglVectorLayerDemo from "@demos/WebglVectorLayerDemo.vue"
import WebglVectorLayerDemo2 from "@demos/WebglVectorLayerDemo2.vue"
</script>

<ClientOnly>
<WebglVectorLayerDemo />
</ClientOnly>

::: code-group

<<< ../../../../src/demos/WebglVectorLayerDemo.vue

:::

### `variables`

You can also filter features according to variables (inspired in this [openlayers example](https://openlayers.org/en/latest/examples/filter-webgl-line.html)).

<ClientOnly>
<WebglVectorLayerDemo2 />
</ClientOnly>

::: code-group

<<< ../../../../src/demos/WebglVectorLayerDemo2.vue

:::

## Properties

### disableHitDetection

- **Type**: `boolean`
- **Default**: `false`

### style

- **Type**: `object`
- **Default**: `() => ({
    'stroke-color' : 'green',
    'stroke-width' : 2
})`

### variables

- **Type**: `object`
