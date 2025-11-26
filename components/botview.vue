<template>
  <div>

    <!-- Floating Chatbot Button -->
    <button
      v-if="!isOpen"
      @click="isOpen = true"
      class="fixed bottom-6 right-6 bg-blue-600 hover:bg-blue-700 text-white p-4 rounded-full shadow-lg transition-all"
    >
      <!-- Avatar Icon -->
      <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none"
        viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round"
          d="M7 8h10M7 12h6m-6 4h4m1 6l-2.5-2.5H7A2 2 0 015 18V6a2 2 0 012-2h10a2 2 0 012 2v12a2 2 0 01-2 2h-4.5L12 22z" />
      </svg>
    </button>

    <!-- Dark overlay -->
    <div
      v-if="isOpen"
      @click="closeChat"
      class="fixed inset-0 bg-black/40 backdrop-blur-sm"
    ></div>

    <!-- Chat Window Popup -->
    <div
      v-if="isOpen"
      class="fixed inset-0 flex items-center justify-center p-4"
    >
      <div class="w-full max-w-md bg-white rounded-3xl shadow-2xl flex flex-col h-[550px] sm:h-[600px] animate-scaleIn relative">

        <!-- Close Button -->
        <button
          @click="closeChat"
          class="absolute top-4 right-4 text-white bg-black/20 hover:bg-black/30 rounded-full p-2 transition"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none"
            viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round"
              d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>

        <!-- History Button -->
        <button
          @click="toggleHistory"
          class="absolute top-4 right-14 text-white bg-black/20 hover:bg-black/30 rounded-full p-2 transition"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none"
            viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round"
              d="M12 6v6l4 2m6-2a10 10 0 11-20 0 10 10 0 0120 0z" />
          </svg>
        </button>

        <!-- Header -->
        <header class="bg-gradient-to-r from-blue-500 to-indigo-600 text-white p-5 rounded-t-3xl text-center shadow-md font-semibold text-xl flex items-center justify-center gap-2">
          <!-- Show human avatar instead of text -->
          <span v-if="!showHistory" class="flex items-center gap-2">
            <!-- Heroicon: User Circle -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round"  d="M12 20a7.966 7.966 0 0 1-5.002-1.756l.002.001v-.683c0-1.794 1.492-3.25 3.333-3.25h3.334c1.84 0 3.333 1.456 3.333 3.25v.683A7.966 7.966 0 0 1 12 20ZM2 12C2 6.477 6.477 2 12 2s10 4.477 10 10c0 5.5-4.44 9.963-9.932 10h-.138C6.438 21.962 2 17.5 2 12Zm10-5c-1.84 0-3.333 1.455-3.333 3.25S10.159 13.5 12 13.5c1.84 0 3.333-1.455 3.333-3.25S13.841 7 12 7Z" clip-rule="evenodd"/>
            </svg>
            Support Agent
          </span>
          <span v-else>Chat History 📜</span>
        </header>


        <!-- MAIN CONTENT AREA -->
        <main ref="chatContainer" class="flex-1 overflow-y-auto p-4 space-y-4">

          <!-- Normal Chat View -->
          <template v-if="!showHistory">
            <div
              v-for="(msg, i) in messages"
              :key="i"
              class="flex"
              :class="msg.role === 'user' ? 'justify-end' : 'justify-start'"
            >
              <div
                class="max-w-xs sm:max-w-sm px-4 py-2 rounded-2xl shadow-md break-words"
                :class="msg.role === 'user' ? 'bg-blue-600 text-white' : 'bg-gray-200 text-gray-900'"
              >
                {{ msg.content }}
              </div>
            </div>

            <!-- Typing Indicator -->
            <div v-if="loading" class="flex justify-start">
              <div class="max-w-xs px-4 py-2 rounded-2xl shadow bg-gray-200 text-gray-700 animate-pulse">
                Typing...
              </div>
            </div>
          </template>

          <!-- HISTORY VIEW -->
          <template v-else>
            <div v-if="history.length === 0" class="text-center text-gray-500">
              No history found.
            </div>

            <div
              v-for="(item, i) in history"
              :key="i"
              class="bg-gray-100 p-3 rounded-xl shadow"
            >
              <p class="text-xs text-gray-500 mb-1">User:</p>
              <p class="p-2 bg-white rounded-lg shadow mb-2">{{ item.userMessage }}</p>

              <p class="text-xs text-gray-500 mb-1">Bot:</p>
              <p class="p-2 bg-blue-100 rounded-lg shadow mb-2">{{ item.botMessage }}</p>

              <p class="text-xs text-gray-400 mt-1 text-right">{{ formatDate(item.createdAt) }}</p>
            </div>
          </template>

        </main>

        <!-- Input (hidden when history view is open) -->
        <form
          v-if="!showHistory"
          @submit.prevent="sendMessage"
          class="p-4 bg-gray-50 rounded-b-3xl flex gap-2 border-t"
        >
          <input
            v-model="input"
            type="text"
            placeholder="Type your message..."
            class="flex-1 p-3 border border-gray-300 rounded-full focus:outline-none focus:ring-2 focus:ring-blue-500"
            :disabled="loading"
          />
          <button
            type="submit"
            class="bg-blue-600 text-white px-6 py-3 rounded-full hover:bg-blue-700 disabled:opacity-50"
            :disabled="loading"
          >
            Send
          </button>
        </form>

      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, nextTick, watch } from "vue";

const isOpen = ref(false);
const showHistory = ref(false);
const messages = ref([
  { role: "assistant", content: "Hi! 👋 Welcome to TrendyShop. How can I help you today?" }
]);
const history = ref([]);

const input = ref("");
const loading = ref(false);
const chatContainer = ref(null);

const API_CHAT = "https://localhost:7155/chat";
const API_HISTORY = "https://localhost:7155/history";

async function sendMessage() {
  if (!input.value.trim() || loading.value) return;

  messages.value.push({ role: "user", content: input.value });
  const userMessage = input.value;

  input.value = "";
  loading.value = true;

  try {
    const res = await $fetch(API_CHAT, {
      method: "POST",
      body: { message: userMessage },
      headers: { "Content-Type": "application/json" }
    });

    messages.value.push({ role: "assistant", content: res.reply });
  } catch (error) {
    console.error(error);
    messages.value.push({
      role: "assistant",
      content: "Oops! Something went wrong."
    });
  } finally {
    loading.value = false;
    await nextTick();
    scrollToBottom();
  }
}

async function toggleHistory() {
  showHistory.value = !showHistory.value;

  if (showHistory.value) {
    try {
      const res = await $fetch(API_HISTORY);
      history.value = res; // array with userMessage, botMessage, createdAt
    } catch (err) {
      console.error(err);
      history.value = [];
    }
  }

  await nextTick();
  scrollToBottom();
}

function closeChat() {
  isOpen.value = false;
  showHistory.value = false; // reset history view
}

function scrollToBottom() {
  if (chatContainer.value) {
    chatContainer.value.scrollTop = chatContainer.value.scrollHeight;
  }
}

// Format timestamp nicely
function formatDate(dateStr) {
  if (!dateStr) return "";
  const d = new Date(dateStr);
  return d.toLocaleString(); // e.g., 11/25/2025, 12:42:09 PM
}

watch(messages, () => nextTick(scrollToBottom));
</script>

<style scoped>
@keyframes scaleIn {
  from { transform: scale(0.85); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}
.animate-scaleIn {
  animation: scaleIn 0.25s ease-out;
}

main::-webkit-scrollbar {
  width: 8px;
}
main::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 0, 0.2);
  border-radius: 4px;
}
main::-webkit-scrollbar-track {
  background: transparent;
}
</style>
