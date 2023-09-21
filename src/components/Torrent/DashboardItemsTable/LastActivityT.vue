<template>
    <div>{{ torrent.last_activity }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'LastActivityT',
  mixins: [TorrentDashboardItem]
})
</script>
