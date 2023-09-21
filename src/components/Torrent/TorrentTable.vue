<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="torrents"
      :page.sync="page"

      @mousedown="hideTorrent"
      @dblclick:row="showInfo"
      @contextmenu:row="RightClickMenu"
      hide-default-footer
      class="elevation-1"
    >

    <template #item.size="{item}">
      <SizeT :torrent="item"/>
    </template>
    <template #item.progress="{item}">
      <ProgressT :torrent="item"/>
    </template>
    <template #item.downloaded="{item}">
      <DownloadedT :torrent="item"/>
    </template>
    <template #item.uploaded="{item}">
      <UploadedT :torrent="item"/>
    </template>
    </v-data-table>
  </div>

</template>

<script>

  import SizeT from './DashboardItemsTable/SizeT.vue'
  import ProgressT from './DashboardItemsTable/ProgressT.vue'
  import DownloadedT from './DashboardItemsTable/DownloadedT'
  import UploadedT from './DashboardItemsTable/UploadedT'
  import { mapState } from 'vuex'
  import { Torrent } from '@/models'
  import { TorrentSelect, General } from '@/mixins'

  export default {
    name: "TorrentTable",
    mixins: [TorrentSelect, General],
    components: {
      SizeT,
      ProgressT,
      DownloadedT,
      UploadedT
    },
    props: {
      torrents: Array,
      heads: Array,
      showTorrentRightClickMenu: Function,
      hideTorrentRightClickMenu: Function,
      strTouchStart: Function,
      srtTouchMove: Function,
      srtTouchEnd: Function
    },
    data () {
      return {
        page: 1,
        pageCount: 0,
        itemsPerPage: 10,
        desserts: this.torrents,
      }
    },
    computed: {

      headers() {
        this.desserts = this.heads.map((properties) => {
          properties.text  = properties.name.toLowerCase();
          properties.value = properties.name.toLowerCase();
          properties.width = 100;
        })
        return this.desserts = [{
          "text": "name",
          "value": "name",
          "width": 300
        },
        ...this.heads
        ]


      },
      test() {
        return this.headers
      }
    },
    methods: {
      showInfo (event, {item}) {
        const hash = (item.hash)
        this.$router.push({ name: 'torrentDetail', params: {hash} })
      },

      RightClickMenu(event, torrent) {
        this.hideTorrentRightClickMenu();
        setTimeout(() => {
          const dataHash = {"torrent": { hash: torrent.item.hash }}
          this.showTorrentRightClickMenu(event, dataHash)
        }, 100);
      },
      hideTorrent() {
        this.hideTorrentRightClickMenu()
      }
    }
  }
</script>
