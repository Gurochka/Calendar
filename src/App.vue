<template>
  <div>
    <AppHeader />
    <mainContent />
  </div>
</template>

<script>
import AppHeader from '@/components/AppHeader.vue'
import mainContent from '@/components/mainContent.vue'

export default {
  components: {
    AppHeader,
    mainContent
  }
}
</script>