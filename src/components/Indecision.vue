<template>
    <img v-if="img" :src="img" alt="bg">
    <div class="bg-dark"></div>

    <div class="indecision-container">
        <input type="text" placeholder="Hazme una pregunta" v-model="question"/>
        <p>Recuerda terminar con un signo de interrogante (?)</p>

        <div>
            <h2>{{ question }}</h2>
            <h1>{{ answer }}</h1>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                question: null,
                answer: null,
                img: null,
            }
        },
        methods: {
            async getAnswer() {
                this.answer = "Pensando...";
                const { answer, image } = await fetch('https://yesno.wtf/api').then(( r => r.json() ));
                
                this.answer = answer;
                this.img = image;
            }
        },
        watch: {
            question( value, oldValue ){
                if( !value.includes('?') ) return
                this.getAnswer();
                //TODO: Realiza HTTP
            }
        },
        computed: {
            answerToSpanish(){
                if(this.answer === 'yes'){
                    return this.answer = 'SI!!'
                };

                if(this.answer === 'no'){
                    return this.answer = 'NO!!'
                };
            }
        }
    }
</script>

<style scope>

.container{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>