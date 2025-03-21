<template>
 
        
    

<div>

      <ScoreBoard />


        <template v-if="this.question">

          <h1
            v-html="this.question"
          ></h1>
      
          <template v-for="(answer, index) in  this.answers" :key="index">
    
    
            <input type="radio" 
            :disabled="this.answerSubmitted"
            name="options"
            :value="answer"
            v-model="this.chosenAnswer"
            >
            <label v-html="answer"></label><br>
            
          </template>
          
          <button v-if="!this.answerSubmitted" @click="this.subimitAnswer" class="send" type="button">Send</button>
          
          
          <section v-if="this.answerSubmitted" class="result">
            <h4 v-if="this.chosenAnswer == this.correctAnswers" v-html= "'&#9989; Congratiulations you pick the right answer.' + this.correctAnswers + 'is correct.'">
                
            </h4>
            <h4 v-else v-html= "'&#10060; I`m sorry, you picked the wrong answer. The correct is' + this.correctAnswers + '.'" >
            
            </h4>

              <button @click="this.getNewQuestion" class="send" type="button">Next question</button>
          </section>
          
          
        </template>

</div> 

</template>


<script>


import ScoreBoard from './components/ScoreBoard.vue';



export default {
  name: 'App',

  components: {
    ScoreBoard
  },


  data(){
      return {
        question: undefined,
        incorrectAnswers: undefined,
        correctAnswers: undefined,
        chosenAnswer: undefined,
        answerSubmitted: false
        
      }
  },
  //METHODS OU COMPUTED PROPERTIES 
  computed: {
      answers() {
        var answers = [...this.incorrectAnswers];
        answers.splice(Math.round(Math.random() *4) ,0 ,this.correctAnswers);
        return answers;
      }
  },

  methods: {

        subimitAnswer(){
              if(!this.chosenAnswer){
                  alert('Pic one of the options')
              } else {
                  this.answerSubmitted = true;
                  if(this.chosenAnswer== this.correctAnswers){
                   console.log('you got it right!')
                  }
                  else{
                    console.log('your answer is wrong')
                  }
              }
        },

        getNewQuestion(){

          this.answerSubmitted = false;
          this.chosenAnswer = undefined;
          this.question = undefined;

          this.axios
                .get('https://opentdb.com/api.php?amount=1')
                .then((response) => {
                  this.question = response.data.results[0].question;
                  this.incorrectAnswers =  response.data.results[0].incorrect_answers;
                  this.correctAnswers=  response.data.results[0].correct_answer;

                  //apenas PEGUE OS DADOS AQUI 
                  console.log(response.data.results[0])
                })
        }
  
  },
  
 created(){

      this.getNewQuestion();
     

 }

  
 
}//na template fica tudo que é visivel na pagina

//toda a logica desse componmente


//https://opentdb.com/api.php?amount=1 api de perguntas
</script>

<style lang="scss">
#app {
  
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

  input[type=radio]{
    margin: 12px 4px;
  }

  button.send{
        color: white;
        background-color:#1867c0;
        border: 1px solid #1867c0;
        cursor: pointer;
        min-width: 120px;
        height: 40px;
        margin-top: 12px;
        padding: 0;
  }
}
</style>
