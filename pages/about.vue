<template>
    <Header/>

  <div class="min-h-screen bg-gray-50">

    <!-- Hero Section -->
    <section class="bg-gradient-to-r from-yellow-600 to-indigo-700 text-white py-20 px-6">
      <div class="max-w-4xl mx-auto text-center">
        <h1 class="text-5xl font-extrabold mb-4 tracking-wide">
          About TrendCommerce
        </h1>
        <p class="text-lg opacity-90 max-w-2xl mx-auto leading-relaxed">
          A modern e-commerce platform built to deliver convenience, quality, and a seamless digital shopping experience.
        </p>
      </div>
    </section>

    <!-- Main About Section -->
    <section class="max-w-6xl mx-auto px-6 py-16">
      <div class="grid md:grid-cols-2 gap-12 items-center">

        <!-- Text -->
        <div>
          <h2 class="text-3xl font-bold text-gray-800 mb-4">Who We Are</h2>
          <p class="text-gray-600 leading-relaxed">
            TrendCommerce is your trusted online marketplace offering fast delivery,
            premium products, and user-friendly services. Our platform is designed
            to provide a smooth shopping experience with powerful search features,
            secure transactions, and responsive customer support.
          </p>

          <p class="text-gray-600 mt-4 leading-relaxed">
            We focus on smart technology, customer-centric service, and consistent innovation
            to help customers shop with confidence and ease.
          </p>
        </div>

        <!-- Image Card -->
        <div class="rounded-2xl shadow-xl overflow-hidden transform hover:scale-105 transition duration-300">
          <img 
            src="https://images.unsplash.com/photo-1542744173-8e7e53415bb0?q=80&w=1200" 
            alt="E-commerce team"
            class="w-full h-80 object-cover"
          />
        </div>
      </div>
    </section>

    <!-- Feature Cards -->
    <section class="bg-white py-16">
      <div class="max-w-6xl mx-auto px-6 text-center">
        <h2 class="text-3xl font-bold text-gray-800">Why Choose TrendCommerce?</h2>
        <p class="text-gray-600 mt-3 mb-10 max-w-2xl mx-auto">
          Trusted by hundreds of customers for fast delivery, quality service, and advanced AI support.
        </p>

        <div class="grid sm:grid-cols-2 md:grid-cols-3 gap-8">

          <div class="p-8 bg-gray-50 rounded-xl shadow hover:shadow-xl transition duration-300">
            <h3 class="text-xl font-semibold text-blue-600 mb-2">🚚 Fast Delivery</h3>
            <p class="text-gray-600">Lightning-fast order processing and nationwide delivery.</p>
          </div>

          <div class="p-8 bg-gray-50 rounded-xl shadow hover:shadow-xl transition duration-300">
            <h3 class="text-xl font-semibold text-blue-600 mb-2">🔒 Secure Payments</h3>
            <p class="text-gray-600">Multiple safe and trusted payment options.</p>
          </div>

          <div class="p-8 bg-gray-50 rounded-xl shadow hover:shadow-xl transition duration-300">
            <h3 class="text-xl font-semibold text-blue-600 mb-2">💬 24/7 Support</h3>
            <p class="text-gray-600">We are always here to help you whenever needed.</p>
          </div>

          <div class="p-8 bg-gray-50 rounded-xl shadow hover:shadow-xl transition duration-300">
            <h3 class="text-xl font-semibold text-blue-600 mb-2">⭐ Quality Products</h3>
            <p class="text-gray-600">Only the top-rated and tested products are listed.</p>
          </div>

          <div class="p-8 bg-gray-50 rounded-xl shadow hover:shadow-xl transition duration-300">
            <h3 class="text-xl font-semibold text-blue-600 mb-2">🔄 Easy Returns</h3>
            <p class="text-gray-600">Simple return process with friendly support.</p>
          </div>

          <div class="p-8 bg-gray-50 rounded-xl shadow hover:shadow-xl transition duration-300">
            <h3 class="text-xl font-semibold text-blue-600 mb-2">🤖 AI Chatbot</h3>
            <p class="text-gray-600">
              Fast, intelligent, and helpful responses powered by AI.
            </p>
          </div>

        </div>

      </div>
    </section>

  </div>

  <BotView/>
  <Footer/>
</template>

<script>
import Header from '@/components/header.vue';
import BotView from '@/components/botview.vue';
import Footer from '@/components/footer.vue';

export default {
  components: {
    Header,
    BotView,
    Footer,
  }
}
</script>

<style scoped>
section {
  animation: fadeIn 0.6s ease-in-out;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
