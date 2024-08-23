<template>
  <ChatPage>
    <template #messages>
      <ChatMessages ref="chatMessages" />
    </template>
    <template #input>
      <ChatInput @send-message="handleSendMessage" />
    </template>
  </ChatPage>
</template>

<script setup lang="ts">
import ChatPage from '~/components/ChatPage.vue'
import ChatInput from '~/components/ChatInput.vue'
import ChatMessages from '~/components/ChatMessages.vue'

const chatMessages = ref()

function handleSendMessage(message: string, sender: 'user' | 'bot') {
  chatMessages.value.addMessage(message, sender)
}
</script>