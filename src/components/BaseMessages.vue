<script setup lang="ts">
import IconCancelStatus from './icons/IconCancelStatus.vue'
type Message = {
  id: number
  description: string
  date: string
  isCanceled: boolean
}

defineProps<{ messages: Message[] }>()

defineEmits(['cancelMessage'])
</script>
<template>
  <div class="row rounded-2 bg wrapper">
    <div class="row my-2 message-wrapper" v-for="message in messages" :key="message.id">
      <div class="col-1">
        <IconCancelStatus v-if="message.isCanceled" />
      </div>
      <div class="col">{{ message.description }}</div>
    </div>
  </div>
</template>
<style scoped>
.bg {
  background-color: #f6f8fa;
}
</style>
