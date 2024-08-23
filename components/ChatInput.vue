<template>
  <form @submit.prevent="sendMessage" class="flex items-center gap-2">
    <UInput
      v-model="message"
      placeholder="Type your message..."
      class="flex-grow"
    />
    <UButton type="submit" color="primary" :disabled="!message.trim() || isLoading">
      {{ isLoading ? 'Sending...' : 'Send' }}
    </UButton>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const message = ref('')
const isLoading = ref(false)
const emit = defineEmits(['send-message'])

async function sendMessage() {
  if (message.value.trim() && !isLoading.value) {
    isLoading.value = true
    emit('send-message', message.value, 'user')
    
    try {
      const response = await $fetch('/api/chat', {
        method: 'POST',
        body: { message: message.value }
      })
      emit('send-message', response.message, 'bot')
    } catch (error) {
      console.error('Error sending message:', error)
      emit('send-message', 'Sorry, I encountered an error. Please try again.', 'bot')
    } finally {
      isLoading.value = false
      message.value = ''
    }
  }
}
</script>