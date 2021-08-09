<template>

    <img v-if="image" :src="image" alt="bg"/>
    <div class="bg-dark">

    </div>

    <div class="indecision-container">
        <h1>Preguntame algo</h1>
        <input v-model="question" type="text" placeholder="Realiza una pregunta...">
        <p>Recuerda que debes de terminar con una interrogación '?'</p>

        <div v-if="isValidQuestion">
            <h2>{{ question }}</h2>
            <h1>{{ answer }}</h1>
        </div>

    </div>

</template>

<script>

export default {

    data() {
        return {
            question: null,
            answer: null,
            image: null,
            isValidQuestion: false
        }
    },

    watch: {
        question( value, old ){

            this.isValidQuestion = false

            console.log( value.includes('?') )
            if ( !value.includes('?') ) return

            this.isValidQuestion = true

            //TODO: Realizar peticion HTTP
            this.getAnswer()
        }
    },

    methods: {

        async getAnswer() {

            this.answer = 'Pensando...'

            const { answer, image } = await fetch('https://yesno.wtf/api').then( resp => resp.json() )
            console.log( answer )

            //Results
            this.answer = answer === 'yes' ? 'sisisisisisi' : 'LOL NO'
            this.image = image
        }

    }

}

</script>

<!--  Scoped - se necesita ponerlo para que se aplique solamente a lo que esta utilizandose  -->
<style scoped>

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
        font-size: 15px;
        margin-top: 20px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>