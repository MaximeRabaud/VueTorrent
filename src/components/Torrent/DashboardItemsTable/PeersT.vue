<template>
    <div>
      {{ torrent.num_leechs }}
      <span class="grey--text caption"> / {{ torrent.available_peers }} </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'PeersT',
  mixins: [TorrentDashboardItem]
})
</script>
