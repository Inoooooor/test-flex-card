<script setup lang="ts">
import { ref, computed } from 'vue'
import IconCancelStatus from './components/icons/IconCancelStatus.vue'
import BaseAlert from './components/BaseAlert.vue'
import BaseMessages from './components/BaseMessages.vue'

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

const messageInput = ref<string>('')

const addMessage = () => {
  if (!messageInput.value) {
    return
  }

  messages.value.push({
    id: Date.now(),
    description: messageInput.value,
    date: 'Date.now()',
    isCanceled: false,
  })

  messageInput.value = ''
}

const submit = (event: Event) => {
  event.preventDefault()
  addMessage()
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
    <base-messages :messages="messages"></base-messages>
    <!-- <div class="row">
      <form @submit="submit">
        <div class="row">
          <div class="col-8">
            <input
              v-model="messageInput"
              type="text"
              class="form-control"
              placeholder="Сообщение"
              aria-label="Сообщение"
            />
          </div>
          <div class="col-4">
            <button
              type="submit"
              class="form-control"
              placeholder="Last name"
              aria-label="Last name"
            >
              Отправить
            </button>
          </div>
        </div>
      </form>
    </div> -->
  </div>
</template>

<style scoped></style>
