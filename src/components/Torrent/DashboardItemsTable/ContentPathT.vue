<template>
    <div>{{ torrent.content_path }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'ContentPathT',
  mixins: [TorrentDashboardItem]
})
</script>
