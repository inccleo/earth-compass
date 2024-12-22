<script setup lang="ts">
import { routeWhiteList } from '@/config/routes'

const route = useRoute()
const router = useRouter()
const { t } = useI18n()

// 定义需要隐藏导航栏的路径
const hideNavBarPaths = ['/map']

function onBack() {
  if (window.history.state.back)
    history.back()
  else
    router.replace('/')
}

const title = computed(() => {
  if (!route.meta)
    return ''

  return route.meta.i18n ? t(route.meta.i18n) : (route.meta.title || '')
})

// 添加显示控制计算属性
const show = computed(() => {
  const currentPath = route.path
  return !hideNavBarPaths.some(path => currentPath.startsWith(path))
})

const showLeftArrow = computed(() => route.name && routeWhiteList.includes(route.name))
</script>

<template>
  <VanNavBar
    v-if="show"
    :title="title"
    :fixed="true"
    clickable
    placeholder
    :left-arrow="!showLeftArrow"
    @click-left="onBack"
  />
</template>
