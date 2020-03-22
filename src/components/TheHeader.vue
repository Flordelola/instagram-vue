<template>
  <header>
    <button v-if="step === 1" @click="handleGoTo">
      <i class="fab fa-instagram fa-2x"></i>
    </button>
    <button v-if="step === 2 || step === 3" @click="handleGoTo">
      <i class="fas fa-arrow-left"></i> Cancel
    </button>
    <button v-if="step === 2" @click="handleNextStep">
      Next <i class="fas fa-arrow-right"></i>
    </button>
    <button v-if="step === 3" @click="handleShare">
      <i class="fas fa-share"></i>
    </button>
  </header>
</template>

<script>
export default {
  name: 'TheHeader',
  props: {
    step: {
      tyle: Number,
      default: 1
    }
  },
  methods: {
    handleGoTo() {
      this.$emit('go-to')
    },
    handleNextStep() {
      this.$emit('next-step')
    },
    handleShare() {
      this.$emit('share-post')
    }
  }
}
</script>

<style lang="css">
  header {
    height: 50px;
    background-color: #041e30;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    padding: 0 20px; 
  }
  header button {
    color: #ffffff;
    font-weight: bold;
    cursor: pointer;
    background: transparent;
    border: none;
  }
</style>