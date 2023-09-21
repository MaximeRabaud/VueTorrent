<template>
    <div>
      {{ torrent.dlspeed | formatSpeedValue(shouldUseBitSpeed()) }}
      <span class="caption grey--text">
        {{ torrent.dlspeed | formatSpeedUnit(shouldUseBitSpeed()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'DownloadSpeedT',
  mixins: [TorrentDashboardItem]
})
</script>
