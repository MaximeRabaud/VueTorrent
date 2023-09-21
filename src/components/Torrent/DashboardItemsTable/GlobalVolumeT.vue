<template>
    <div>
      {{ torrent.globalVolume | formatDataValue(shouldUseBinaryData()) }}
      <span class="caption grey--text">
        {{ torrent.globalVolume | formatDataUnit(shouldUseBinaryData()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'GlobalVolumeT',
  mixins: [TorrentDashboardItem]
})
</script>
