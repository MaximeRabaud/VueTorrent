<template>
    <div>{{ torrent.completed_on }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'CompletedOnT',
  mixins: [TorrentDashboardItem]
})
</script>
