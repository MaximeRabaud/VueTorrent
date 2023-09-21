<template>
    <div>
      {{ torrent.globalSpeed | formatSpeedValue(shouldUseBitSpeed()) }}
      <span class="caption grey--text">
        {{ torrent.globalSpeed | formatSpeedUnit(shouldUseBitSpeed()) }}
      </span>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'GlobalSpeed',
  mixins: [TorrentDashboardItem]
})
</script>
