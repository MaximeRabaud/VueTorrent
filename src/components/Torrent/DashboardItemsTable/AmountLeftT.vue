<template>
    <div>
      {{ torrent.amount_left | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.amount_left | formatDataUnit(shouldUseBinaryData()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'AmountLeftT',
  mixins: [TorrentDashboardItem]
})
</script>
