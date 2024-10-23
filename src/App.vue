<template>
  <div class="location-input">
    <h2>Find artikler tæt på dig!</h2>
    <p>Indtast, hvor mange kilometer du ønsker fra det valgte postnummer.</p>

    <div class="input-group">
      <input
        type="number"
        id="max-distance"
        v-model="maxDistance"
        placeholder="50"
        class="distance-input"
      />
      <span>km fra</span>
      <input
        type="text"
        id="postal-code"
        v-model="postalCode"
        placeholder="8000"
        class="postal-input"
      />
    </div>

    <button @click="submit" class="submit-btn">Vis</button>

    <div v-if="submitted" class="submitted-data">
      <p>Items for sale in your location:</p>
      <p>{{ itemsCount }}</p>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const maxDistance = ref(50); // Default to 50km
    const postalCode = ref('8000'); // Default postal code
    const submitted = ref(false);

    const itemsCount = computed(() => {
      if (maxDistance.value <= 10) {
        return 10;
      } else if (maxDistance.value > 10 && maxDistance.value <= 20) {
        return 40;
      } else if (maxDistance.value > 20) {
        return 1000;
      }
      return 0; // Default to 0 if no match
    });

    const submit = () => {
      if (postalCode.value && maxDistance.value) {
        submitted.value = true;
      } else {
        alert('Please fill out both fields.');
      }
    };

    return {
      maxDistance,
      postalCode,
      submitted,
      submit,
      itemsCount,
    };
  },
};
</script>

<style scoped>
.location-input {
  max-width: 400px;
  margin: 20px auto;
  text-align: center;
  padding: 20px;
  background-color: #3c808c; /* Matching background color */
  border-radius: 10px;
  color: white;
}

h2 {
  font-size: 1.5em;
  margin-bottom: 10px;
}

p {
  margin-bottom: 15px;
}

.input-group {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.distance-input,
.postal-input {
  width: 70px;
  padding: 10px;
  font-size: 1.1em;
  border-radius: 5px;
  border: none;
}

.distance-input {
  text-align: center;
}

.postal-input {
  text-align: center;
}

.submit-btn {
  padding: 10px 20px;
  font-size: 1.1em;
  background-color: #ffffff;
  color: #3c808c;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.submit-btn:hover {
  background-color: #e3e3e3;
}

.submitted-data {
  margin-top: 20px;
}
</style>
