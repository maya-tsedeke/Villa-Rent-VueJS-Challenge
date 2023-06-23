<template>
  <div class="villa-container">
    <div class="villa-card" v-for="villa in displayedVillas" :key="villa.id" @click="selectVilla(villa)">
      <img class="villa-thumbnail" :src="villa.thumbnail" alt="Villa Thumbnail" />
      <div class="villa-details">
        <h3>{{ villa.location }}</h3>
        <p>Price: {{ villa.price }}</p>
        <p>Capacity: {{ villa.capacity }}</p>
        <p>Facilities: {{ villa.facilities }}</p>
        <button class="villa-book-btn" @click.stop="selectVilla(villa)">Book</button>
      </div>
    </div>
    <div class="load-more-container">
      <button v-if="displayedVillas.length < villas.length" @click="loadMore" class="load-more-btn">Load More</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['villas'],
  data() {
    return {
      displayedVillas: [],
      displayAmount: 3,
      selectedVilla: null,
      showModal: false
    };
  },
  mounted() {
    this.loadVillas();
  },
  methods: {
    loadVillas() {
      this.displayedVillas = this.villas.slice(0, this.displayAmount);
    },
    loadMore() {
      this.displayAmount += 3;
      this.loadVillas();
    },
    selectVilla(villa) {
      this.$emit('select-villa', villa);
    }
  }
};
</script>

<style scoped>
@import './css/DisplayVilla.css';
</style>
