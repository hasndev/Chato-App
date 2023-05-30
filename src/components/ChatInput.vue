<template>
	<div class="p-2 flex items-center py-2 bg-white border-t">
		<textarea @keyup.enter.exact="sendMessage" v-model="messageText"
			class="flex-1 bg-gray-200 rounded-lg p-2 text-sm resize-none" placeholder="Type your message..."></textarea>
		<button class="send-button bg-blue-500 text-white px-4 py-2 rounded-lg font-bold ml-3" @click="sendMessage">
			Send
		</button>
	</div>
</template>
  
<script setup>
import { ref, onMounted } from 'vue';

const messageText = ref('');
const emit = defineEmits(['send']);

const sendMessage = () => {
	if (messageText.value.trim() !== '') {
		emit('send', messageText.value);
		messageText.value = '';
	}
};

onMounted(() => {
	messageText;
	sendMessage;
})
</script>