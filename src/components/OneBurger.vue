<template>
    <div>
      <h4> {{ burger.name }} </h4> 
      <img v-bind:src="burger.imageURL" alt="Span" title="test" style="width: 200px">
                <ul>
                    
                    <span v-if="burger.containsGluten">
                      <li>Innehåller gluten</li>
                    </span>
                    <span v-if="burger.containsLactose">
                      <li> Innehåller laktos </li>
                    </span>
                    <li> {{burger.kCal}} kcal </li>
                    <button type="submit" id="increasebutton" v-on:click="amountOrdered++" style="width: 20px">
                     +
                    </button>
                    <button type="submit" id="decreasebutton" v-if="amountOrdered > 0" v-on:click="amountOrdered--" style="width: 20px">
                     -
                    </button>
                    <h4> Amount: {{amountOrdered}} </h4>
                  
                    <button type="submit" id="confirmorder" v-if="amountOrdered > 0" v-on:click="addBurger" style="width: 75px">
                     Add to cart
                    </button>
                    
                </ul>
    </div>
            
  </template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    },
    data: function () {
      return {
        amountOrdered: 0,
        
      }
    },
    methods: {
    addBurger: function () {
      this.amountOrdered;
      this.$emit('orderedBurger', { name:   this.burger.name, 
                                    amount: this.amountOrdered 
                                  }
      );
    }
  }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
    .Gluten {
        font-weight: bold;
        color: blueviolet;
    }
    .Laktos {
        font-weight: bold;
        color: mediumvioletred;
    }
    div * {
    margin-left: 10px;
    margin-top: 1px;
    }
    .wrapper {
    display: grid;
    grid-gap: 10px;
    grid-template-columns: 200px 200px 200px;
    
    }
  </style>
  