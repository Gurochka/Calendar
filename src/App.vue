<template>
  <div>
    <appHeader />
    <mainContent />
  </div>
</template>

<script>
import appHeader from '@/components/appHeader.vue'
import mainContent from '@/components/mainContent.vue'

export default {
  components: {
    appHeader,
    mainContent
  }
}
</script>