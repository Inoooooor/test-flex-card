<script setup lang="ts">
import { ref } from 'vue'
const input = ref('')

const emit = defineEmits(['submit'])

const handleSubmit = (event: Event) => {
  event.preventDefault()
  if (!input.value) {
    return
  }
  emit('submit', input.value)

  input.value = ''
}
</script>
<template>
  <div class="row">
    <form class="form px-0" @submit="handleSubmit">
      <div class="row">
        <div class="col-8">
          <input
            v-model="input"
            type="text"
            class="form-control"
            placeholder="Сообщение"
            aria-label="Сообщение"
          />
        </div>
        <div class="col-4">
          <button
            type="submit"
            class="form-control button"
            placeholder="Last name"
            aria-label="Last name"
          >
            Отправить
          </button>
        </div>
      </div>
    </form>
  </div>
</template>
<style scoped>
.button {
  background: linear-gradient(to left, #04694b, #11a87b) !important;
  color: white;
  overflow-wrap: anywhere;
}
</style>
