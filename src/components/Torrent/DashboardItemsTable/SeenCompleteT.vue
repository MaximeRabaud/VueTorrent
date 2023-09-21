<template>
    <div>{{ torrent.seen_complete }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'SeenCompleteT',
  mixins: [TorrentDashboardItem]
})
</script>
