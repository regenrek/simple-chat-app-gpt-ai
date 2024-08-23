<template>
  <UContainer class="h-screen flex flex-col">
    <UCard class="flex-grow overflow-hidden flex flex-col">
      <template #header>
        <h2 class="text-xl font-bold">Chat App</h2>
      </template>
      <div class="flex-grow overflow-y-auto p-4">
        <slot name="messages"></slot>
      </div>
      <template #footer>
        <slot name="input"></slot>
      </template>
    </UCard>
  </UContainer>
</template>