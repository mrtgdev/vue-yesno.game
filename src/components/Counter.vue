<template>

  <h2> {{ customTitle }} </h2>
  <p>{{ counter }} <sup>2</sup> = {{ squareCounter }} </p>

  <div>
    <button @click="decrease">-1</button>
    <button @click="increase">+1</button>
  </div>

</template>

<script>
export default {

  props: {
    title: String,
    start: {
      type: Number,
      required: true,
      validator( value ) {
        return value > 10
      }
    }
  },

  data() {
    return {
      counter: this.start
    }
  },

  methods: {
    getSquareValue( value ) {
      return (value * value)
    },
    increase() {
      console.log('Aumenta el valor')
      this.counter++
    },
    decrease() {
      console.log('Desciende el valor')
      this.counter--
    }
  },

  //Se guardan en el caché los componentes computados,
  //- Solo se va ejecutar una sola vez cada vez que se llame a la funcion 
  computed: {
    squareCounter() {
      console.log('This is a computed - Square Counter')
      return this.counter * this.counter
    },
    customTitle() {
      return this.title ? this.title : 'Counter'
    }
  }
  
}
</script>

<style>

button {
  background-color: rgb(13, 185, 110);
  border-radius: 5px;
  border: 1px solid white;
  color: white;
  padding: 5px 15px;
  margin: 5px;
  transition: 0.3s ease-in-out;
}

button:hover {
  background-color: #5aa75b;
  transition: 0.3s ease-in-out
}

</style>