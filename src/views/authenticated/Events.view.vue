<script setup>
import { ref } from 'vue';

const events = ref([
  { title: 'Webinar: AI in Healthcare', date: 'Sep 10, 2025', time: '2:00 PM', category: 'Webinar', description: 'Explore the impact of AI in modern healthcare.' },
  { title: 'Virtual Job Fair', date: 'Sep 14, 2025', time: '11:00 AM', category: 'Job Fair', description: 'Connect with top companies looking for talent.' },
  { title: 'Python Bootcamp', date: 'Sep 20, 2025', time: '9:00 AM', category: 'Workshop', description: 'Learn Python from scratch in an interactive bootcamp.' },
  { title: 'Data Science Conference', date: 'Oct 2, 2025', time: '10:00 AM', category: 'Conference', description: 'Join top data scientists and researchers at the annual conference.' },
  { title: 'Startup Pitch Event', date: 'Oct 10, 2025', time: '1:00 PM', category: 'Meetup', description: 'Meet founders pitching their startups to investors.' }
]);

const isModalVisible = ref(false);
const selectedEvent = ref(null);

const openModal = (event) => {
  selectedEvent.value = event;
  isModalVisible.value = true;
};

const closeModal = () => {
  isModalVisible.value = false;
};
</script>

<template>
  <section class="bg-white rounded-lg shadow-lg p-6">
    <h3 class="text-2xl font-semibold mb-6">Upcoming Events</h3>

    <div class="flex gap-3 mb-6">
      <button class="px-6 py-3 text-sm text-white bg-indigo-600 rounded-lg hover:bg-indigo-700 transition duration-300 ease-in-out transform hover:scale-105">
        All Events
      </button>
      <button class="px-6 py-3 text-sm text-white bg-gray-600 rounded-lg hover:bg-gray-700 transition duration-300 ease-in-out transform hover:scale-105">
        Webinars
      </button>
      <button class="px-6 py-3 text-sm text-white bg-gray-600 rounded-lg hover:bg-gray-700 transition duration-300 ease-in-out transform hover:scale-105">
        Workshops
      </button>
    </div>

    <ul class="space-y-4">
      <li v-for="event in events" :key="event.title" class="flex justify-between items-center bg-gray-50 p-4 rounded-lg shadow-md hover:shadow-lg transition duration-300 ease-in-out transform hover:scale-105">
        <div>
          <h4 class="text-lg font-medium text-gray-800">{{ event.title }}</h4>
          <p class="text-sm text-gray-500">{{ event.date }} – {{ event.time }}</p>
          <p class="text-sm text-gray-600 mt-2">{{ event.description }}</p>
        </div>
        <button
          @click="openModal(event)"
          class="bg-indigo-600 text-white text-sm px-4 py-2 rounded-md hover:bg-indigo-700 transition duration-300 ease-in-out transform hover:scale-105"
        >
          Join
        </button>
      </li>
    </ul>
  </section>

  <div v-if="isModalVisible" class="fixed inset-0 bg-gray-500 bg-opacity-90 flex items-center justify-center z-50 transition duration-300 ease-in-out">
    <div class="bg-white rounded-lg p-8 max-w-lg w-full shadow-lg">
      <h4 class="text-2xl font-semibold text-gray-800">{{ selectedEvent?.title }}</h4>
      <p class="text-sm text-gray-500">{{ selectedEvent?.date }} – {{ selectedEvent?.time }}</p>
      <p class="text-sm text-gray-600 mt-3">{{ selectedEvent?.description }}</p>
      <div class="mt-6 flex justify-end">
        <button @click="closeModal" class="bg-gray-600 text-white text-sm px-6 py-3 rounded-md hover:bg-gray-700 transition duration-300 ease-in-out transform hover:scale-105">
          Close
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.fixed {
  z-index: 9999;
}

button:hover {
  transform: translateY(-2px);
  transition: all 0.2s;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
