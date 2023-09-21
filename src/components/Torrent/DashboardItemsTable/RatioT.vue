<template>
    <div>{{ torrent.ratio }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'RatioT',
  mixins: [TorrentDashboardItem]
})
</script>
