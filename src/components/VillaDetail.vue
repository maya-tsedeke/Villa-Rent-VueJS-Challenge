<template>
  <div class="villa-page">
    <div class="villa-slider">
      <div class="slider-wrapper" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
        <div v-for="(image, index) in villa.images" :key="index" class="slider-item" :class="{ active: currentIndex === index }">
          <img :src="image" alt="Villa Image" />
          <div class="slider-facility">{{ villa.facilities[index] }}</div>
        </div>
      </div>
      <div class="slider-controls">
        <button class="slider-control prev" @click="prevSlide">
          Previous
        </button>
        <button class="slider-control next" @click="nextSlide">
          Next
        </button>
      </div>
    </div>

    <div class="villa-details">
      <h2>{{ villa.name }}</h2>
      <p class="villa-location">Location: {{ villa.location }}</p>
      <p class="villa-price">Price: {{ villa.price }}</p>
      <p class="villa-description">Description: {{ villa.description }}</p>

      <!-- More villa details, capacity, features, etc. -->

      <div class="villa-buttons">
        <button @click="showConfirmationModal">Book</button>
        <button @click="goBack">Back</button>
      </div>
    </div>

    <!-- Confirmation Modal -->
    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <h2>Confirmation</h2>
        <p>Are you sure you want to book {{ villa.name }}?</p>
        <div class="modal-buttons">
          <button @click="confirmBooking">Confirm</button>
          <button @click="closeConfirmationModal">Cancel</button>
        </div>
      </div>
    </div>

    <!-- Success Message -->
    <div v-if="showSuccessMessage" class="modal">
      <div class="modal-content">
        <h2>Booking Successful!</h2>
        <p>Thank you for booking {{ villa.name }}.</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['villa'],
  data() {
    return {
      currentIndex: 0,
      showModal: false,
      showSuccessMessage: false
    };
  },
  computed: {
    images() {
      return this.villa.images || [];
    }
  },
  methods: {
    showConfirmationModal() {
      this.showModal = true;
    },
    closeConfirmationModal() {
      this.showModal = false;
    },
    confirmBooking() {
      this.showSuccessMessage = true;
      this.closeConfirmationModal();
      setTimeout(() => {
        this.goBack();
      }, 2000);
    },
    goBack() {
      this.$emit('go-back');
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
    },
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    }
  }
};
</script>

<style>
@import './css/villaDetail.css';
</style>
