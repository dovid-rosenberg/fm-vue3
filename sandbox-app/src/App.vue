<script>
  export default{
    data:() => ({
      count: 0,
      counterTitle: 'Counter Standard',
      incrementAmount: 10
    }),
    computed: {
      displayTitle() {
        if (this.count > 20) {
          return 'Counter Very Long'
        }
        return 'Counter Standard'
      },
      optimizedIncrementAmount () {
        return this.displayTitle.length * this.incrementAmount
      }
    },
    methods: {
      incrementCount(newAmount, event) {
        this.count += this.optimizedIncrementAmount
      },
    },
    watch: {
      count(newValue) {

      }
    }
  }
</script>

<template>
    <div class="wrapper">
      <h1>{{ displayTitle }}</h1>
      <p>{{ count }}</p>
      <button @click="incrementCount(10, $event)">Add</button>
      <div>
        <label for="incrementAmount">Increment by:</label>
        <input id="incrementAmount" type="number" v-model="incrementAmount">
      </div>

      <hr />

    </div>
</template>
