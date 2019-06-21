<template>
  <div>
    <AppHeader />
    <MainContent />
  </div>
</template>

<script>
import AppHeader from '@/components/AppHeader.vue'
import MainContent from '@/components/MainContent.vue'

export default {
  components: {
    AppHeader,
    MainContent
  }
}
</script>