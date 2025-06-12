<template>
  <div class="min-h-screen bg-gray-50 flex">
    <!-- Sidebar -->
    <div class="w-80 bg-white border-r border-gray-200 flex flex-col">
      <!-- Header -->
      <div class="p-4 border-b border-gray-200">
        <div class="flex items-center justify-between mb-4">
          <h1 class="text-xl font-bold text-gray-900">Tuition Wave</h1>
          <div class="flex items-center space-x-2">
            <button class="p-2 hover:bg-gray-100 rounded-lg">
              <Icon name="heroicons:bell" class="w-5 h-5 text-gray-600" />
            </button>
            <div class="flex items-center space-x-2">
              <img src="https://images.pexels.com/photos/220453/pexels-photo-220453.jpeg?auto=compress&cs=tinysrgb&w=40&h=40&fit=crop&crop=face" 
                   alt="Guardian" class="w-8 h-8 rounded-full">
              <span class="text-sm font-medium text-gray-700">Guardian Name</span>
            </div>
          </div>
        </div>
        
        <!-- Navigation -->
        <nav class="space-y-1">
          <NuxtLink to="/" class="flex items-center space-x-3 px-3 py-2 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors">
            <Icon name="heroicons:home" class="w-5 h-5" />
            <span class="text-sm">Home</span>
          </NuxtLink>
          <a href="#" class="flex items-center space-x-3 px-3 py-2 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors">
            <Icon name="heroicons:magnifying-glass" class="w-5 h-5" />
            <span class="text-sm">Find Tutor</span>
          </a>
          <a href="#" class="flex items-center space-x-3 px-3 py-2 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors">
            <Icon name="heroicons:document-text" class="w-5 h-5" />
            <span class="text-sm">My Request</span>
          </a>
          <a href="#" class="flex items-center space-x-3 px-3 py-2 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors">
            <Icon name="heroicons:user" class="w-5 h-5" />
            <span class="text-sm">My Tutor</span>
          </a>
          <a href="#" class="flex items-center space-x-3 px-3 py-2 text-white bg-blue-500 rounded-lg">
            <Icon name="heroicons:chat-bubble-left-right" class="w-5 h-5" />
            <span class="text-sm font-medium">Message</span>
          </a>
          <a href="#" class="flex items-center space-x-3 px-3 py-2 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors">
            <Icon name="heroicons:cog-6-tooth" class="w-5 h-5" />
            <span class="text-sm">Settings</span>
          </a>
        </nav>
      </div>
      
      <!-- Search -->
      <div class="p-4 border-b border-gray-200">
        <div class="relative">
          <Icon name="heroicons:magnifying-glass" class="absolute left-3 top-1/2 transform -translate-y-1/2 w-4 h-4 text-gray-400" />
          <input 
            type="text" 
            placeholder="Search name, chat, etc"
            class="w-full pl-10 pr-4 py-2 bg-gray-100 border-0 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-sm"
          >
        </div>
      </div>
      
      <!-- Chat List -->
      <div class="flex-1 overflow-y-auto">
        <div class="space-y-1 p-2">
          <div 
            v-for="chat in chatList" 
            :key="chat.id"
            @click="selectChat(chat)"
            :class="['flex items-center space-x-3 p-3 rounded-lg cursor-pointer transition-colors',
                     selectedChat?.id === chat.id ? 'bg-blue-50 border-l-4 border-blue-500' : 'hover:bg-gray-50']"
          >
            <div class="relative">
              <img :src="chat.avatar" :alt="chat.name" class="w-12 h-12 rounded-full">
              <div v-if="chat.unreadCount" class="absolute -top-1 -right-1 w-5 h-5 bg-blue-500 text-white text-xs rounded-full flex items-center justify-center">
                {{ chat.unreadCount }}
              </div>
            </div>
            <div class="flex-1 min-w-0">
              <div class="flex items-center justify-between">
                <h3 class="text-sm font-medium text-gray-900 truncate">{{ chat.name }}</h3>
                <span class="text-xs text-gray-500">{{ chat.time }}</span>
              </div>
              <p class="text-sm text-gray-600 truncate mt-1">{{ chat.lastMessage }}</p>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Logout -->
      <div class="p-4 border-t border-gray-200">
        <button class="flex items-center space-x-3 px-3 py-2 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors w-full">
          <Icon name="heroicons:arrow-left-on-rectangle" class="w-5 h-5" />
          <span class="text-sm">Logout</span>
        </button>
      </div>
    </div>

    <!-- Main Chat Area -->
    <div class="flex-1 flex flex-col">
      <!-- Chat Header -->
      <div v-if="selectedChat" class="bg-white border-b border-gray-200 p-4">
        <div class="flex items-center justify-between">
          <div>
            <h2 class="text-lg font-semibold text-gray-900">Message</h2>
            <p class="text-sm text-gray-600">Find and explore various types of tutors</p>
          </div>
          <div class="flex items-center space-x-2">
            <img :src="selectedChat.avatar" :alt="selectedChat.name" class="w-10 h-10 rounded-full">
            <div>
              <h3 class="text-sm font-medium text-gray-900">{{ selectedChat.name }}</h3>
              <p class="text-xs text-gray-500">{{ selectedChat.status }}</p>
            </div>
            <button class="p-2 hover:bg-gray-100 rounded-lg ml-4">
              <Icon name="heroicons:ellipsis-horizontal" class="w-5 h-5 text-gray-600" />
            </button>
          </div>
        </div>
      </div>

      <!-- Messages Area -->
      <div v-if="selectedChat" class="flex-1 overflow-y-auto p-4 bg-gray-50">
        <div class="max-w-4xl mx-auto space-y-4">
          <!-- Date Separator -->
          <div class="text-center">
            <span class="bg-white px-4 py-1 rounded-full text-xs text-gray-500 border">Yesterday</span>
          </div>
          
          <!-- Messages -->
          <div v-for="message in messages" :key="message.id" class="space-y-4">
            <div :class="['flex', message.sender === 'me' ? 'justify-end' : 'justify-start']">
              <div :class="['flex space-x-3 max-w-2xl', message.sender === 'me' ? 'flex-row-reverse space-x-reverse' : '']">
                <img 
                  :src="message.sender === 'me' ? currentUserAvatar : selectedChat.avatar" 
                  :alt="message.sender === 'me' ? 'You' : selectedChat.name"
                  class="w-8 h-8 rounded-full flex-shrink-0"
                >
                <div :class="['rounded-2xl px-4 py-3 max-w-md', 
                             message.sender === 'me' ? 'bg-blue-500 text-white' : 'bg-white text-gray-900']">
                  <p class="text-sm">{{ message.text }}</p>
                  <div class="flex items-center justify-between mt-2">
                    <span :class="['text-xs', message.sender === 'me' ? 'text-blue-100' : 'text-gray-500']">
                      {{ message.time }}
                    </span>
                    <div v-if="message.sender === 'me'" class="flex space-x-1">
                      <Icon name="heroicons:check" class="w-3 h-3 text-blue-100" />
                      <Icon name="heroicons:check" class="w-3 h-3 text-blue-100" />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Message Input -->
      <div v-if="selectedChat" class="bg-white border-t border-gray-200 p-4">
        <div class="max-w-4xl mx-auto">
          <div class="flex items-center space-x-4">
            <div class="flex-1 relative">
              <input 
                v-model="newMessage"
                @keypress.enter="sendMessage"
                type="text" 
                placeholder="Type a message..."
                class="w-full px-4 py-3 bg-gray-100 border-0 rounded-full focus:outline-none focus:ring-2 focus:ring-blue-500 pr-12"
              >
              <button class="absolute right-3 top-1/2 transform -translate-y-1/2 p-1 hover:bg-gray-200 rounded-full">
                <Icon name="heroicons:paper-clip" class="w-5 h-5 text-gray-500" />
              </button>
            </div>
            <button 
              @click="sendMessage"
              class="bg-blue-500 hover:bg-blue-600 text-white p-3 rounded-full transition-colors"
            >
              <Icon name="heroicons:paper-airplane" class="w-5 h-5" />
            </button>
          </div>
        </div>
      </div>

      <!-- Empty State -->
      <div v-else class="flex-1 flex items-center justify-center bg-gray-50">
        <div class="text-center">
          <Icon name="heroicons:chat-bubble-left-right" class="w-16 h-16 text-gray-400 mx-auto mb-4" />
          <h3 class="text-lg font-medium text-gray-900 mb-2">Select a conversation</h3>
          <p class="text-gray-600">Choose a chat from the sidebar to start messaging</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// SEO
useHead({
  title: 'Messages - Tuition Wave',
  meta: [
    { name: 'description', content: 'Chat with tutors and manage your conversations on Tuition Wave.' }
  ]
})

// Current user avatar
const currentUserAvatar = 'https://images.pexels.com/photos/220453/pexels-photo-220453.jpeg?auto=compress&cs=tinysrgb&w=40&h=40&fit=crop&crop=face'

// Chat list data
const chatList = ref([
  {
    id: 1,
    name: 'Lucas Murphy',
    avatar: 'https://images.pexels.com/photos/1222271/pexels-photo-1222271.jpeg?auto=compress&cs=tinysrgb&w=40&h=40&fit=crop&crop=face',
    lastMessage: 'I have some dietary restrictions and would like to know if the Parisian',
    time: '3:45 PM',
    unreadCount: 1,
    status: 'last seen recently'
  },
  {
    id: 2,
    name: 'Osman Farooq',
    avatar: 'https://images.pexels.com/photos/1681010/pexels-photo-1681010.jpeg?auto=compress&cs=tinysrgb&w=40&h=40&fit=crop&crop=face',
    lastMessage: 'I have some dietary restrictions and would like to know if the Parisian',
    time: 'Yesterday',
    unreadCount: 0,
    status: 'last seen recently'
  },
  {
    id: 3,
    name: 'Sarah Johnson',
    avatar: 'https://images.pexels.com/photos/1239291/pexels-photo-1239291.jpeg?auto=compress&cs=tinysrgb&w=40&h=40&fit=crop&crop=face',
    lastMessage: 'Thank you for the session today!',
    time: '2:30 PM',
    unreadCount: 0,
    status: 'online'
  },
  {
    id: 4,
    name: 'Mike Chen',
    avatar: 'https://images.pexels.com/photos/1043471/pexels-photo-1043471.jpeg?auto=compress&cs=tinysrgb&w=40&h=40&fit=crop&crop=face',
    lastMessage: 'Can we reschedule tomorrow\'s lesson?',
    time: '1:15 PM',
    unreadCount: 2,
    status: 'last seen 2 hours ago'
  }
])

// Selected chat and messages
const selectedChat = ref(null)
const newMessage = ref('')

// Sample messages for the selected chat
const messages = ref([
  {
    id: 1,
    sender: 'other',
    text: 'Hello, I had an amazing time on the Venice Dreams package! Could you please help me with booking a similar trip to Rome for next spring? Thanks!',
    time: '10:15 AM'
  },
  {
    id: 2,
    sender: 'me',
    text: 'Hi Osman! We\'re thrilled to hear that you enjoyed the Venice Dreams package. We would be happy to assist you in booking a similar trip to Rome for next spring. Do you have specific dates in mind?',
    time: '10:20 AM'
  },
  {
    id: 3,
    sender: 'other',
    text: 'Thank you! I\'m looking at the first two weeks of April. Is there a package available during that time?',
    time: '10:25 AM'
  },
  {
    id: 4,
    sender: 'me',
    text: 'Yes, we have a Rome Highlights package available from April 1 to April 14. It includes visits to historic sites, a guided tour of the Colosseum, and a day trip to Vatican City. Would you like more details?',
    time: '10:30 AM'
  },
  {
    id: 5,
    sender: 'other',
    text: 'That sounds perfect. Could you please send me the itinerary and pricing details?',
    time: '10:35 AM'
  },
  {
    id: 6,
    sender: 'me',
    text: 'Sure! I\'ll email you the full itinerary and pricing details for the Rome Highlights package. Please check your inbox shortly. If you have any other questions, feel free to ask.',
    time: '10:40 AM'
  },
  {
    id: 7,
    sender: 'other',
    text: 'Got it, thank you! I\'ll review the details and get back to you soon.',
    time: '10:45 AM'
  }
])

// Functions
const selectChat = (chat) => {
  selectedChat.value = chat
  // Mark as read
  chat.unreadCount = 0
}

const sendMessage = () => {
  if (newMessage.value.trim() && selectedChat.value) {
    const message = {
      id: messages.value.length + 1,
      sender: 'me',
      text: newMessage.value.trim(),
      time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
    }
    messages.value.push(message)
    newMessage.value = ''
    
    // Update last message in chat list
    const chatIndex = chatList.value.findIndex(c => c.id === selectedChat.value.id)
    if (chatIndex !== -1) {
      chatList.value[chatIndex].lastMessage = message.text
      chatList.value[chatIndex].time = message.time
    }
  }
}

// Auto-select first chat on mount
onMounted(() => {
  if (chatList.value.length > 0) {
    selectChat(chatList.value[1]) // Select Osman Farooq by default
  }
})
</script>