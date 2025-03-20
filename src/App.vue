<template>
 
<div>
  
      <h1
        v-html="this.question"
      ></h1>

  <input type="radio" name="options" value="True">
  <label>True</label><br>

  <input type="radio" name="options" value="False">
  <label>False</label><br>

  <button class="send" type="button">Send</button>

</div> 

</template>

<script>


export default {
  name: 'App',

  data(){
      return {
        question: undefined,
        incorrectAnswers: undefined,
        correctAnswers: undefined
      }
  },
  
 created(){


      this.axios
      .get('https://opentdb.com/api.php?amount=1')
      .then((response) => {
        this.question = response.data.results[0].question;
        this.incorrectAnswers =  response.data.results[0].incorrect_answers;
        this.correctAnswers=  response.data.results[0].correct_answer;


        console.log(response.data.results[0])
      })

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
