<template>

  <section class="src-components-container-comp">

    <div id="container">

      <div 
        class="square" 
        v-for="(square, index) in this.$store.state.squares" 
        :style="square.style" 
        :key="index" 
        @click="verificarColor(square.style)"
      ></div>

    </div>

  </section>

</template>

<script>

  export default  {
    name: 'src-components-container-comp',
    mounted () {
    },
    data () {
      return {
        message: ''
      }
    },
    methods: {
      verificarColor(styleP){
        let {backgroundColor} = styleP
        if ( backgroundColor === this.$store.state.pickedColor) {
              this.message = "You Picked Right!"
              this.sendMessage()
              this.setAllColorsTo(this.$store.state.pickedColor);
              this.$store.dispatch('msgRestartBtn', "Play Again!")
              this.$store.dispatch('setWin', true)
            } else {
              this.message = "Try Again!";
              this.sendMessage()
              styleP.backgroundColor = "#232323"
            }
      },
      setAllColorsTo(color) {
        this.$store.state.squares.forEach((e) => e.style= { ...e.style, backgroundColor:color})
      },
      sendMessage(){
        this.$store.dispatch('guardarMessage', this.message)
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  

  .square {
	width: 30%;
	background: blue;
	padding-bottom: 30%;
	float: left;
	margin: 1.66%;
	border-radius: 10%;
	transition: background 0.8s;
	-webkit-transition: background 0.8s;
	-moz-transition: background 0.8s;
}

  #container {
    margin: 20px auto;
    max-width: 600px;
  }

</style>
