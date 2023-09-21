<template>
    <div>{{ torrent.infohash_v1 }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'InfoHashV1T',
  mixins: [TorrentDashboardItem]
})
</script>
