<template>
    <v-chip style="height: 1.3em" class="caption white--text px-2" :class="torrentStateClass">
      {{ stateString }}
    </v-chip>
</template>

<script lang="ts">
import { TorrentDashboardItem } from '@/mixins'
import { defineComponent } from 'vue'
import { TorrentState } from '@/enums/vuetorrent'

export default defineComponent({
  name: 'StatusT',
  mixins: [TorrentDashboardItem],
  computed: {
    stateString() {
      if (!this.torrent) return TorrentState.UNKNOWN

      let finalState = this.torrent.state.toString()
      if (this.torrent.forced) {
        finalState = `[F] ${finalState}`
      }

      return finalState
    }
  }
})
</script>
