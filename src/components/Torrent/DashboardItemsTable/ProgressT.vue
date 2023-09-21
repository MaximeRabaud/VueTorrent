<template>
    <v-progress-linear :value="torrent?.progress ?? 0" height="20" style="width: 90%" :color="`torrent-${torrentStateClass}`" rounded>
      <span class="caption white--text">{{ torrent.progress | progress }}</span>
    </v-progress-linear>
</template>

<script lang="ts">
import { TorrentDashboardItem } from '@/mixins'
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ProgressT',
  mixins: [TorrentDashboardItem]
})
</script>
