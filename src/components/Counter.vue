<template>
  <div class="counter">
    <h2>{{ customTitle }}</h2>
    <p> {{ counter }} <sub>2</sub> = {{ squareCounter }}  </p>
    <button @click="increase">+1</button>
    <button @click="decrease">-1</button>
  </div>
</template>

<script>
export default {
    props: {
        title: String,
        start: {
            type: Number,
            default: 5,
            //required: true
            validator( value ) {
                return value > 100
            }
        },
    },

    data() {
        return {
            counter: this.start
        }
    },
    methods: {
        getSquareValue(){
            return this.counter * this.counter
        },
        increase() {
            this.counter++;
        },
        decrease() {
            this.counter--;
        }
    },
    computed: {
        squareCounter() {
            return this.counter * this.counter
        },
        customTitle() {
            return this.title || 'Counter'
        }
    }
}
</script>

<style>

    .counter{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        gap: 10px;
    }

    button{
        background-color: #64BB87;
        border-radius: 5px;
        border: 1 solid white;
        color: white;
        cursor: pointer;
        margin: 0 5px;
        padding: 5px 15px;
        transition: 0.3s ease-in-out;
    }

    button:hover {
        background-color: #5aa67b;
        transition: 0.3s ease-in-out ;
    }

</style>