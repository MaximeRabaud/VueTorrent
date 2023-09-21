<template>
    <div>
      {{ torrent.uploaded | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.uploaded | formatDataUnit(shouldUseBinaryData()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'UploadedT',
  mixins: [TorrentDashboardItem]
})
</script>
