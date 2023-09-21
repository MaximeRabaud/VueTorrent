<template>
    <div>
      {{ torrent.downloaded_session | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.downloaded_session | formatDataUnit(shouldUseBinaryData()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'DownloadedSessionT',
  mixins: [TorrentDashboardItem]
})
</script>
