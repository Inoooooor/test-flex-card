<script setup lang="ts">
import { ref, computed } from 'vue'
import IconCancelStatus from './components/icons/IconCancelStatus.vue'
import BaseAlert from './components/BaseAlert.vue'
import BaseMessages from './components/BaseMessages.vue'
import BaseMessagesForm from './components/BaseMessagesForm.vue'

type Message = {
  id: number
  description: string
  date: string
  isCanceled: boolean
}

const messages = ref<Message[]>([
  {
    id: 1,
    description: 'Сообщение 1',
    date: '2000-20-02',
    isCanceled: false,
  },
  {
    id: 2,
    description: 'Сообщение 2',
    date: '2000-20-02',
    isCanceled: false,
  },
  {
    id: 3,
    description: 'Сообщение 3',
    date: '2000-20-02',
    isCanceled: false,
  },
])

const currentMessageIndex = ref(0)

const allowedMessages = computed(() => {
  return messages.value.filter((message) => !message.isCanceled)
})

const currentMessage = computed(() => {
  const newCurrentIndex = (currentMessageIndex.value + 1) % messages.value.length
  return allowedMessages.value[newCurrentIndex] || 'Ничего'
})

const addMessage = (value: string) => {
  messages.value.push({
    id: Date.now(),
    description: value,
    date: 'Date.now()',
    isCanceled: false,
  })
}

const submit = (value: string) => {
  addMessage(value)
}

const cancelMessage = (id: Message['id']) => {
  const message = messages.value.find((message) => message.id === id)

  if (!message) {
    return
  }
  message.isCanceled = true
}

const messageTimer = 2000
setInterval(() => currentMessageIndex.value++, messageTimer)
</script>

<template>
  <div class="container w-50 mx-auto shadow-lg rounded-2 p-4">
    <base-alert
      class="mb-4"
      :message="currentMessage"
      @cancel-message="cancelMessage(currentMessage.id)"
    ></base-alert>
    <base-messages :messages="messages" class="mb-4"></base-messages>
    <base-messages-form @submit="submit" />
  </div>
</template>

<style scoped></style>
