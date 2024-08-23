<template>
  <div class="space-y-4">
    <div
      v-for="(msg, index) in messages"
      :key="index"
      class="flex items-start"
      :class="msg.sender === 'user' ? 'justify-end' : 'justify-start'"
    >
      <UAvatar
        v-if="msg.sender === 'bot'"
        src="https://api.dicebear.com/6.x/bottts/svg?seed=bot"
        alt="Bot"
        class="mr-2"
      />
      <UCard
        :class="msg.sender === 'user' ? 'bg-primary-100' : 'bg-gray-100'"
        class="max-w-[70%]"
      >
        <p>{{ msg.text }}</p>
      </UCard>
      <UAvatar
        v-if="msg.sender === 'user'"
        src="https://api.dicebear.com/6.x/avataaars/svg?seed=user"
        alt="User"
        class="ml-2"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Message {
  text: string
  sender: 'user' | 'bot'
}

const messages = ref<Message[]>([])

const addMessage = (text: string, sender: 'user' | 'bot') => {
  messages.value.push({ text, sender })
}

defineExpose({ addMessage })
</script>