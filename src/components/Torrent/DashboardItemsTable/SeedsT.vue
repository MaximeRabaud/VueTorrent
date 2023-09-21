<template>
    <div>
      {{ torrent.num_seeds }}
      <span class="grey--text caption"> / {{ torrent.available_seeds }} </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'SeedsT',
  mixins: [TorrentDashboardItem]
})
</script>
