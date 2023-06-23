<template>
  <div id="app">
    <nav>
      <ul>
        <li @click="switchComponent('DisplayVillas')" :class="{ active: currentComponent === 'DisplayVillas' }">
          Browse Villas
        </li>
        <li v-if="selectedVilla" @click="switchComponent('VillaDetail')"
          :class="{ active: currentComponent === 'VillaDetail' }">
          Villa Detail
        </li>
      </ul>
    </nav>

    <div class="content">
      <component :is="currentComponent" :villas="villas" :villa="selectedVilla" @select-villa="showVillaDetail"
        @book-villa="showConfirmationModal" @go-back="goBack" />
    </div>
  </div>
</template>

<script>
import DisplayVillas from './components/DisplayVillas.vue';
import VillaDetail from './components/VillaDetail.vue';
import { Samplevillas } from './components/sampleVillas.js';
export default {
  name: 'App',
  components: {
    DisplayVillas,
    VillaDetail
  },
  data() {
    return {
      villas:Samplevillas,
      selectedVilla: null,
      currentComponent: 'DisplayVillas'
    };
  },
  methods: {
    switchComponent(componentName) {
      this.currentComponent = componentName;
    },
    showVillaDetail(villa) {
      this.selectedVilla = villa;
      this.currentComponent = 'VillaDetail';
    },
    showConfirmationModal(villa) {
      console.log('Book villa:', villa);
    },
    goBack() {
      this.selectedVilla = null;
      this.currentComponent = 'DisplayVillas';
    }
  }
};
</script>
<style>
@import 'common.css';
</style>

