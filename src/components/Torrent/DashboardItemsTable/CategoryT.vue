<template>
    <v-chip small class="upload white--text caption">
      {{ torrent.category }}
    </v-chip>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { TorrentDashboardItem } from '@/mixins'

export default defineComponent({
  name: 'CategoryT',
  mixins: [TorrentDashboardItem]
})
</script>
