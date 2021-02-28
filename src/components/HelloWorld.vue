<template>
  <div>
    <h2 class="title">Calcul en Pourcentage</h2>

    <label for="basicPrice"
      >basicPrice:
      <input
        id="basicPrice"
        placeholder="Prix de base"
        v-model.lazy="basicPrice"
        @focus="resetBasicPrice()"
      />
    </label>

    <label for="percentage"
      >percentage:
      <input
        id="percentage"
        placeholder="Remise en pourcentage"
        v-model="percentage"
        @focus="resetPercentage()"
      />
    </label>

    <h2>
      Résultat:
      {{ result }}
    </h2>
    <h2>
      Reste:
      {{ rest }}
    </h2>
    <animated-number
      :value="value"
      :formatValue="formatToPrice"
      :duration="300"
    />

    <!-- <input v-model="number">
    <animated-number :number="number"></animated-number> -->

    <!-- <button-counter></button-counter> -->

    <!-- 
      
      

    
     -->
  </div>
</template>
<script>
import AnimatedNumber from 'animated-number-vue'

export default {
  components: {
    AnimatedNumber,
  },
  data() {
    return {
      value: 1000,
      basicPrice: 0,
      percentage: 0,
      number: 0,
    }
  },
  computed: {
    result() {
      return (this.basicPrice * this.percentage) / 100
    },
    rest() {
      return this.basicPrice - this.result
    },
  },
  mounted() {
    console.log('Je démarre')

    setTimeout(() => {
      this.basicPrice = 10
      this.percentage = 5
    }, 1000)
  },

  beforeUpdate() {
    console.log("J'ai changé")
  },

  destroyed() {
    console.log('Je détruis')
  },

  methods: {
    formatToPrice(value) {
      return 'R$ ' + value.toFixed(2)
    },
    resetBasicPrice() {
      if (this.percentage > 0 && this.basicPrice === 0) return
      this.resetCustomValues()
    },
    resetPercentage() {
      if (this.basicPrice > 0 && this.percentage === 0) return
      this.resetCustomValues()
    },
    resetCustomValues() {
      this.percentage = 0
      this.basicPrice = 0
    },
  },
}
</script>
