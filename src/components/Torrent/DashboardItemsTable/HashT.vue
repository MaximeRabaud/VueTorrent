<template>
    <div>{{ torrent.hash }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'HashT',
  mixins: [TorrentDashboardItem]
})
</script>
