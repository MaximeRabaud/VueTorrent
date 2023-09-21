<template>
  <div>
    {{ torrent.added_on }}
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'AddedOnT',
  mixins: [TorrentDashboardItem]
})
</script>
