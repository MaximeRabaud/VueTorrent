<template>
    <div>
      {{ availability }}
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'AvailabilityT',
  mixins: [TorrentDashboardItem],
  computed: {
    availability() {
      if (this.torrent && this.torrent.availability !== -1) {
        return this.torrent.availability
      }

      return 'N/A'
    }
  }
})
</script>
