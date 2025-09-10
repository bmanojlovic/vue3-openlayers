# ol-interaction-synchronize

> Synchronize interaction from ol-ext that allows synchronizing multiple maps

[[toc]]

## Demo

<script setup lang="ts">
import SynchronizeDemo from "@demos/SynchronizeDemo.vue"
</script>

<ClientOnly>
<SynchronizeDemo/>
</ClientOnly>

## Setup

<!--@include: ../../interactions.plugin.md-->

## Usage

| Plugin Usage                  |             Explicit Import              |
| ----------------------------- | :--------------------------------------: |
| `<ol-interaction-synchronize>` | `<Interactions.OlInteractionSynchronize>` |

::: code-group

<<< ../../../../src/demos/SynchronizeDemo.vue

:::

## Properties

### maps

- **Type**: `Array<Map>`
- **Default**: `[]`
- **Description**: Array of maps to synchronize with the current map

## Features

- Synchronizes view center, zoom level, and rotation between maps
- Shows cursor position on all synchronized maps
- Automatically handles map interactions and updates
