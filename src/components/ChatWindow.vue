<template>
	<div class="flex-1 p-4 bg-gray-200">
		<div class="bg-[#4267b2] p-4 rounded-t-lg">
			<h2 v-if="selectedConversation" class="text-white text-lg font-bold">{{ selectedConversation.name }}</h2>
		</div>
		<div class="p-4 bg-white max-h-[44.5rem] overflow-y-auto">
			<ul class="list-none p-0 m-0">
				<li v-for="message in selectedConversation ? selectedConversation.messages : []" :key="message.id"
					:class="['mb-4', message.fromMe ? 'items-right' : '']">
					<div v-if="message.fromMe" :class="['flex mb-4', message.fromMe ? 'justify-end' : '']">
						<div class="flex flex-col max-w-[80%]">
							<div
								:class="['whitespace-pre-wrap p-2 px-3 inline-block rounded-lg', message.fromMe ? 'bg-[#4267b2] text-white' : 'bg-gray-200 text-black']">
								<pre class="whitespace-pre-wrap" v-text="message.text"></pre>
							</div>
							<div class="p-2 px-3 text-right">{{ message.fromMe ? 'han_dev' : selectedConversation.username
							}}</div>
						</div>
						<div class="w-10 h-10 rounded-full ms-2">
							<img :src="selectedConversation.avatar" alt="Avatar" class="w-full h-full rounded-full">
						</div>
					</div>
					<div v-else :class="['flex mb-4', message.fromMe ? 'justify-end' : '']">

						<div class="w-10 h-10 rounded-full me-2">
							<img :src="selectedConversation.avatar" alt="Avatar" class="w-full h-full rounded-full">
						</div>
						<div class="flex flex-col max-w-[80%]">
							<div
								:class="['whitespace-pre-wrap p-2 px-3 inline-block rounded-lg', message.fromMe ? 'bg-[#4267b2] text-white' : 'bg-gray-200 text-black']">
								<pre class="text-base whitespace-pre-wrap" v-text="message.text"></pre>
							</div>
							<div class="p-2 px-3">{{ message.fromMe ? 'han_dev' : selectedConversation.username
							}}</div>
						</div>
					</div>
				</li>
			</ul>
		</div>
	</div>
</template>
  
<script setup>
import { ref, watch } from 'vue';

const messages = ref([]);

const props = defineProps({
	selectedConversation: {
		type: Object,
		required: true,
	},
})

watch(() => props.selectedConversation, () => {
	if (props.selectedConversation) {
		messages.value = [...props.selectedConversation.messages];
	} else {
		messages.value = [];
	}
});

const sendMessage = (messageText) => {
	if (props.selectedConversation && messageText.trim() !== '') {
		const newMessage = {
			id: props.selectedConversation.messages.length + 1,
			fromMe: true,
			text: messageText,
		};
		props.selectedConversation.messages.push(newMessage);
	}
};
</script>