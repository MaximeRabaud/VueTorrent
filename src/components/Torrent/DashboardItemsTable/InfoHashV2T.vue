<template>
    <div>{{ torrent.infohash_v2 }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'InfoHashV2T',
  mixins: [TorrentDashboardItem]
})
</script>
