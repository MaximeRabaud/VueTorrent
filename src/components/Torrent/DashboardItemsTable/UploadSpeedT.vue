<template>
    <div>
      {{ torrent.upspeed | formatSpeedValue(shouldUseBitSpeed()) }}
      <span class="caption grey--text">
        {{ torrent.upspeed | formatSpeedUnit(shouldUseBitSpeed()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'UploadSpeedT',
  mixins: [TorrentDashboardItem]
})
</script>
