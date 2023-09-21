<template>
    <div>{{ torrent.download_path }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'DownloadPathT',
  mixins: [TorrentDashboardItem]
})
</script>
