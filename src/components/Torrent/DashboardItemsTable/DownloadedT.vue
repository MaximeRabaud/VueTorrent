<template>
   <div>
     {{ torrent.downloaded | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.downloaded | formatDataUnit(shouldUseBinaryData()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'DownloadedT',
  mixins: [TorrentDashboardItem]
})
</script>
