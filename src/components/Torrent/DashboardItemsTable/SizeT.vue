<template>
    <div>
      {{ torrent.size | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.size | formatDataUnit(shouldUseBinaryData()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'SizeT',
  mixins: [TorrentDashboardItem]
})
</script>
