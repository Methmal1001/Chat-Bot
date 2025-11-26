<template>
    <Header/>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center px-6 py-12">

    <!-- Page Title -->
    <h1 class="text-4xl font-extrabold text-gray-900 mb-8 text-center">
      Contact <span class="text-blue-600">TrendCommerce</span>
    </h1>

    <!-- Main Container -->
    <div class="w-full max-w-4xl bg-white p-8 rounded-2xl shadow-lg">

      <!-- Description -->
      <p class="text-gray-700 mb-6 leading-relaxed text-center">
        Have questions, feedback, or need support? Our team is always here to help. 
        Fill out the form below and we’ll get back to you shortly.
      </p>

      <div class="grid md:grid-cols-2 gap-8">

        <!-- Contact Form -->
        <form @submit.prevent="submitForm" class="space-y-6">
          <div>
            <label class="block text-gray-800 font-semibold mb-1">Name</label>
            <input
              v-model="form.name"
              type="text"
              required
              class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-blue-400 focus:outline-none"
              placeholder="John Doe"
            />
          </div>

          <div>
            <label class="block text-gray-800 font-semibold mb-1">Email</label>
            <input
              v-model="form.email"
              type="email"
              required
              class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-blue-400 focus:outline-none"
              placeholder="example@email.com"
            />
          </div>

          <div>
            <label class="block text-gray-800 font-semibold mb-1">Message</label>
            <textarea
              v-model="form.message"
              required
              rows="5"
              class="w-full p-3 border rounded-lg focus:ring-2 focus:ring-blue-400 focus:outline-none"
              placeholder="Write your message here..."
            ></textarea>
          </div>

          <button
            type="submit"
            class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 rounded-lg shadow transition"
          >
            Send Message
          </button>
        </form>

        <!-- Contact Info & Map -->
        <div class="space-y-6">

          <!-- Contact Info Card -->
          <div class="bg-gradient-to-r from-blue-500 to-purple-600 text-white p-6 rounded-2xl shadow-lg hover:shadow-2xl transition">
            <h3 class="text-2xl font-bold mb-4 text-center">TrendCommerce Support</h3>

            <p class="flex items-center gap-2 mb-2"><span>📍</span> No. 23, High Street, Colombo, Sri Lanka</p>
            <p class="flex items-center gap-2 mb-2"><span>☎️</span> +94 77 123 4567</p>
            <p class="flex items-center gap-2 mb-2"><span>✉️</span> support@trendcommerce.com</p>
            <p class="flex items-center gap-2"><span>🕒</span> Mon–Fri: 9:00 AM – 6:00 PM</p>
          </div>

          <!-- Map -->
          <div class="rounded-2xl overflow-hidden shadow-lg hover:shadow-2xl transition">
            <iframe
              class="w-full h-64"
              src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3960.123456!2d79.857!3d6.927!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3ae259d2!2sColombo!5e0!3m2!1sen!2slk!4v1691234567890!5m2!1sen!2slk"
              allowfullscreen=""
              loading="lazy"
            ></iframe>
          </div>

        </div>
      </div>
    </div>
  </div>
  <BotView/>
  <Footer/>
</template>

<script setup>
import { ref } from 'vue';
import Header from '@/components/header.vue';
import BotView from '@/components/botview.vue';
import Footer from '@/components/footer.vue';

const form = ref({
  name: '',
  email: '',
  message: '',
});

const submitForm = () => {
  alert(`Thank you, ${form.value.name}! Your message has been sent successfully.`);
  form.value = { name: '', email: '', message: '' };
};
</script>

<style scoped>
/* Fade in animation for section */
div {
  animation: fadeUp 0.6s ease-in-out;
}

@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
