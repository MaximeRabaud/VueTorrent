<script setup lang="ts">
import { useDialog } from '@/composables'
import { ContentLayout } from '@/constants/qbit/AppPreferences'
import { useMaindataStore, useRssStore } from '@/stores'
import { FeedRule } from '@/types/qbit/models'
import { computed, onBeforeMount, reactive, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { VForm } from 'vuetify/components'

const props = defineProps<{
  guid: string
  initialRule?: FeedRule
}>()

const { isOpened } = useDialog(props.guid)
const { t } = useI18n()
const maindataStore = useMaindataStore()
const rssStore = useRssStore()

const form = ref<VForm>()
const isFormValid = ref(false)
const formData = reactive({
  addPaused: null,
  affectedFeeds: [] as string[],
  assignedCategory: '',
  enabled: true,
  episodeFilter: '',
  ignoreDays: 0,
  lastMatch: '',
  mustContain: '',
  mustNotContain: '',
  name: '',
  savePath: '',
  smartFilter: false,
  torrentContentLayout: null,
  useRegex: false
})
const lastSavedName = ref('')
const matchingArticles = ref<{ type: string; value?: string }[]>([])

const addPausedOptions = [
  { title: t('common.useGlobalSettings'), value: null },
  { title: t('constants.addPaused.always'), value: true },
  { title: t('constants.addPaused.never'), value: false }
]
const contentLayoutOptions = [
  { title: t('common.useGlobalSettings'), value: null },
  { title: t('constants.contentLayout.original'), value: ContentLayout.ORIGINAL },
  { title: t('constants.contentLayout.subfolder'), value: ContentLayout.SUBFOLDER },
  { title: t('constants.contentLayout.nosubfolder'), value: ContentLayout.NO_SUBFOLDER }
]
const categories = computed(() => {
  return [{ title: t('common.none'), value: '' }, ...maindataStore.categories.map(category => ({
    title: category.name,
    value: category.name
  }))]
})

const lastMatch = computed(() => {
  if (formData.lastMatch === '') return t('dialogs.rss.rule.lastMatch.unknownValue').toString()

  const delta = new Date().getTime() - new Date(formData.lastMatch).getTime()
  return t('dialogs.rss.rule.lastMatch.knownValue', Math.floor(delta / (1000 * 60 * 60 * 24)).toString())
})
const hasInitialRule = computed(() => {
  return !!(props.initialRule && props.initialRule.name)
})

async function updateArticles() {
  if (lastSavedName.value === '') return

  const formattedArticles = []
  const articles = await rssStore.fetchMatchingArticles(lastSavedName.value)
  for (const feedName in articles) {
    const feedArticles = articles[feedName]
    if (formattedArticles.length > 0) formattedArticles.push({ type: 'divider' })

    formattedArticles.push({ type: 'subheader', value: feedName })

    for (const i in feedArticles) {
      const article = feedArticles[i]
      formattedArticles.push({ type: 'item', value: article })
    }
  }

  matchingArticles.value = formattedArticles
}

async function setRule() {
  if (!isFormValid.value) return

  if ((hasInitialRule.value || lastSavedName.value !== '') && lastSavedName.value !== formData.name) {
    await rssStore.renameRule(lastSavedName.value, formData.name)
  }

  await rssStore.setRule(formData.name, formData)
  lastSavedName.value = formData.name
  await rssStore.fetchRules()
  await updateArticles()
}

async function selectNone() {
  formData.affectedFeeds = []
}

async function selectAll() {
  formData.affectedFeeds = rssStore.feeds.map(feed => feed.url)
}

const close = () => {
  isOpened.value = false
}

onBeforeMount(async () => {
  await maindataStore.fetchCategories()
  await rssStore.fetchRules()
  if (hasInitialRule.value) {
    lastSavedName.value = props.initialRule!.name!
    Object.assign(formData, props.initialRule!)
  } else {
    form.value?.reset()
  }

  await updateArticles()
})
</script>

<template>
  <v-dialog v-model="isOpened">
    <v-card>
      <v-card-title>
        <v-toolbar color="transparent" :title="$t(`dialogs.rss.rule.title.${initialRule ? 'edit' : 'create'}`)">
          <v-btn icon="mdi-close" @click="close" />
        </v-toolbar>
      </v-card-title>
      <v-card-text>
        <v-form v-model="isFormValid" ref="form" @submit.prevent>
          <v-row>
            <v-col cols="12" sm="6" class="scrollable-col">
              <v-text-field v-model="formData.name" autofocus required :label="$t('dialogs.rss.rule.name')" />

              <v-divider />

              <v-checkbox v-model="formData.useRegex" hide-details :label="$t('dialogs.rss.rule.useRegex')" />
              <v-text-field v-model="formData.mustContain" :label="$t('dialogs.rss.rule.mustContain')" />
              <v-text-field v-model="formData.mustNotContain" :label="$t('dialogs.rss.rule.mustNotContain')" />
              <v-checkbox v-model="formData.smartFilter" hide-details :label="$t('dialogs.rss.rule.smartFilter')" />
              <v-text-field v-model="formData.episodeFilter"
                            :placeholder="$t('dialogs.rss.rule.episodeFilterPlaceholder')"
                            :label="$t('dialogs.rss.rule.episodeFilter')" />

              <v-divider class="mb-4" />

              <v-select v-model="formData.assignedCategory" :items="categories"
                        :label="$t('dialogs.rss.rule.assignedCategory')" />
              <v-text-field v-model="formData.savePath" :placeholder="$t('dialogs.rss.rule.savePathPlaceholder')"
                            :label="$t('dialogs.rss.rule.savePath')" />
              <v-text-field v-model="formData.ignoreDays" type="number" :hint="$t('dialogs.rss.rule.ignoreDaysHint')"
                            :label="$t('dialogs.rss.rule.ignoreDays')" />
              <v-text-field v-model="lastMatch" disabled :label="$t('dialogs.rss.rule.lastMatch.label')" />

              <v-divider />

              <v-select v-model="formData.addPaused" :items="addPausedOptions"
                        :label="$t('constants.addPaused.title')" />
              <v-select v-model="formData.torrentContentLayout" :items="contentLayoutOptions"
                        :label="$t('constants.contentLayout.title')" />

              <v-list-subheader>{{ $t('dialogs.rss.rule.affectedFeedsSubheader') }}</v-list-subheader>

              <v-row>
                <v-col cols="6" class="d-flex align-center justify-center">
                  <v-btn color="accent" @click="selectAll">{{ $t('common.selectAll') }}</v-btn>
                </v-col>
                <v-col cols="6" class="d-flex align-center justify-center">
                  <v-btn color="primary" @click="selectNone">{{ $t('common.selectNone') }}</v-btn>
                </v-col>
              </v-row>

              <v-checkbox v-for="item in rssStore.feeds" v-model="formData.affectedFeeds" multiple hide-details
                          :label="item.name" :value="item.url" />
            </v-col>

            <v-divider :vertical="!$vuetify.display.mobile" />

            <v-col cols="12" sm="6" class="scrollable-col">
              <div class="v-card-title pa-0">{{ $t('dialogs.rss.rule.matchingArticles.title') }}</div>
              <v-list>
                <template v-for="item in matchingArticles">
                  <v-divider v-if="item.type === 'divider'" />
                  <v-list-subheader inset v-else-if="item.type === 'subheader'">{{ item.value }}</v-list-subheader>
                  <v-list-item v-else class="mb-3">{{ item.value }}</v-list-item>
                </template>
                <v-list-item v-if="matchingArticles.length === 0"
                             :title="$t('dialogs.rss.rule.matchingArticles.noMatch')" />
              </v-list>
            </v-col>
          </v-row>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn color="error" @click="close">{{ $t('common.close') }}</v-btn>
        <v-btn color="accent" @click="setRule">{{ $t('common.save') }}</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<style scoped>
.scrollable-col {
  @media (min-width: 600px) {
    max-height: calc(100vh - 200px);
  }

  @media (max-width: 599px) {
    max-height: calc(60vh - 200px);
  }

  overflow-y: auto;
}
</style>
