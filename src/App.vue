<template>
  <div class="flex h-screen">
    <div class="flex-shrink-0 w-64 bg-[#4267b2] text-white p-4">
      <h1 class="text-2xl font-bold mb-4">Chato App</h1>
      <ul class="p-0 m-0">
        <li v-for="conversation in conversations" :key="conversation.id" class="flex items-center mb-4 cursor-pointer"
          @click="selectConversation(conversation)">
          <div class="w-10 h-10 rounded-full">
            <img :src="conversation.avatar" alt="Avatar" class="w-full h-full rounded-full">
          </div>
          <div class="ml-3">
            <h2 class="text-lg font-bold">{{ conversation.name }}</h2>
            <p class="text-sm text-gray-300">{{ conversation.message }}</p>
          </div>
        </li>
      </ul>
    </div>
    <div class="flex-1 p-4 bg-gray-200 max-h-screen">
      <ChatWindow :selectedConversation="selectedConversation" />
      <ChatInput @send="sendMessage" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import ChatWindow from './components/ChatWindow.vue';
import ChatInput from './components/ChatInput.vue';

const conversations = ref([
  {
    id: 1,
    name: 'Ali Karrar',
    username: 'ali97',
    avatar: 'https://www.hasndev.com/user-avatar.webp',
    message: 'Hello!',
    messages: [
      { id: 1, fromMe: false, text: 'Hello there!' },
      { id: 2, fromMe: true, text: 'Hi, how can I help you?' },
    ],
  },
  {
    id: 2,
    name: 'Ahmed Mohammed',
    username: 'ahmed90',
    avatar: 'https://www.hasndev.com/user-avatar.webp',
    message: 'Hi there!',
    messages: [
      { id: 1, fromMe: false, text: 'Nice to meet you!' },
      { id: 2, fromMe: true, text: 'Likewise!' },
    ],
  },
]);

const selectedConversation = ref({
  id: 1,
  name: 'Ali Karrar',
  username: 'ali97',
  avatar: 'https://www.hasndev.com/user-avatar.webp',
  message: 'Hello!',
  messages: [
    { id: 1, fromMe: false, text: 'Hello there!' },
    { id: 2, fromMe: true, text: 'Hi, how can I help you?' },
  ],
});

const selectConversation = (conversation) => {
  selectedConversation.value = conversation;
};

const sendMessage = (messageText) => {
  if (selectedConversation.value && messageText.trim() !== '') {
    const newMessage = {
      id: selectedConversation.value.messages.length + 1,
      fromMe: true,
      text: messageText,
    };
    selectedConversation.value.messages.push(newMessage);
  }
};
</script>
