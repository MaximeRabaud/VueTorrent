<template>
    <div>
      {{ torrent.dl_limit | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.dl_limit | formatDataUnit(shouldUseBinaryData()) }}
      </span>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'DownloadLimitT',
  mixins: [TorrentDashboardItem]
})
</script>
