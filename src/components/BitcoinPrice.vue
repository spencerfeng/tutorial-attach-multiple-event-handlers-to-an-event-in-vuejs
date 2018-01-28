<template>
  <div>
    <div>
      <strong>Current Bitcoin price is: </strong>{{ pricePool[currentPriceIndex] }} AUD
    </div>
    <div>
      <button @click="getCurrentPrice">Show Current Price</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BitcoinPrice',
  data () {
    return {
      pricePool: [
        '13676.86',
        '15764.21',
        '19439.80',
        '18905.46',
        '12897.65',
      ],
      currentPriceIndex: 0,
    }
  },
  methods: {
    getCurrentPrice() {
      let requestResultStatusSwitch = Math.floor(Math.random() * 2);

      // succeeded
      if (requestResultStatusSwitch === 1) {
        this.currentPriceIndex++;
        if (this.currentPriceIndex == this.pricePool.length) {
          this.currentPriceIndex = 0;
        }
        this.currentPrice = this.pricePool[this.currentPriceIndex];

        this.$emit('price-request-returned', {
          message: 'The current Bitcoin price has been successfully updated.',
          success: true,
        });
      }
      
      // failed
      if (requestResultStatusSwitch === 0) {
        this.$emit('price-request-returned', {
          message: 'Sorry, something is wrong. Please try again later.',
          success: false,
        });
      }

    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
