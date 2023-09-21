<template>
    <div>
      {{ torrent.up_limit | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.up_limit | formatDataUnit(shouldUseBinaryData()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'UploadLimitT',
  mixins: [TorrentDashboardItem]
})
</script>
