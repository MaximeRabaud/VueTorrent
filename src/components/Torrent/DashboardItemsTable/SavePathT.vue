<template>
    <div class="truncate" :title="torrent?.savePath">
      {{ torrent.savePath }}
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'SavePathT',
  mixins: [TorrentDashboardItem]
})
</script>
