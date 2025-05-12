<script setup lang="ts">
import IconCancel from './icons/IconCancel.vue'
type Message = {
  id: number
  description: string
  date: string
  isCanceled: boolean
}

defineProps<{ message: Message }>()

defineEmits(['cancelMessage'])
</script>
<template>
  <div class="row px-3 py-4 rounded-2 alert-bg">
    <button
      @click="$emit('cancelMessage')"
      class="col-1 p-0 d-flex justify-content-center align-items-center border-0 no-bg"
    >
      <IconCancel />
    </button>
    <span class="col">{{ message.description }}</span>
  </div>
</template>
<style>
.alert-bg {
  background-color: #e4f0ed;
}

.no-bg {
  background-color: transparent;
}
</style>
