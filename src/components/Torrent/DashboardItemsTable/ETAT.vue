<template>
    <div>
      {{ torrent.eta }}
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'ETAT',
  mixins: [TorrentDashboardItem]
})
</script>
