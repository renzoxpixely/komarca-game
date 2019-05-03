<template>
  <div class="tutorial-screen">
    <h1> ¿CÓMO JUGAR?</h1>
    <p>
      Enter The Cosmos es un juego de rol basado en turnos.
Durante tu turno, puedes elegir atacar, sanar o usar un ataque especial.
¡Una vez que realices una acción, tu enemigo también la realizará!
al final de cada nivel se mostrará respuestas por unos cuantos segundos
para que al finalizar completes el cuestionario
</p>
<h1>Controles:</h1>
 <p>
Puedes hacer clic en los botones del héroe o usar los siguientes comandos:
<br>
 - Ataque: (A)
<br>
 - Curar: (H)
<br>
 - Ataque especial: (S)
<br>
También puede omitir pantallas presionando Enter!
 </p>


<h1>Subir de nivel:</h1>
 <p>
 Cada vez que derrotas a un enemigo, ganas algo de experiencia. Dada la suficiente experiencia,
vas a subir de nivel!

Si subes de nivel, tu poder de ataque aumenta. ¡También curarás más y tu barra de salud se repondrá!


¡Prepárate para entrar en el cosmos!
    </p>
    <!--<div class="tutorial-content" v-html="tutorialContent">

    </div>-->
    <!-- TODO: Add instructiosn for global keypresses -->
    <button type="button" v-on:click="changeView('homeScreen')"> Return </button>
  </div>
</template>

<script>
  import bucket from '../../../config/config.js'
  const Cosmic = require('cosmicjs')
  const api = Cosmic()

  export default {
    props: [],
    data() {
      return {
        tutorialContent: ''
      }
    },
    components: {},
    mounted() {
      this.loadTutorialContent()
    },
    computed: {},
    methods: {
      changeView(view) {
        this.$store.commit('changeView', view)
      },
      async loadTutorialContent() {
        const slug = 'tutorial'
        try {
          const res = await bucket.getObject({ slug })
          this.tutorialContent = res.object.content
        } catch(e) {
          console.log('Error getting Tutorial Object', e)
        }
      }
    },
    watch: {}
  }

</script>

<style scoped>
  .tutorial-screen {
    background-color: black;
    height: 100%;
    background-repeat: no-repeat;
    background-size: 100% 100%;
    color: #92ced6;
    padding: 50px;
  }

  .tutorial-screen h1 {
    margin: 0;
    background: black;
    text-decoration: underline;
  }

  .tutorial-screen p {
    font-size: 36px;
    background: black;
  }

  .tutorial-screen button {
    background: black;
    font-size: 36px;
    padding: 20px 40px;
    border: 1px solid #92ced6;
    color: #92ced6;
  }

  .tutorial-content {
    font-size: 36px;
  }
</style>
