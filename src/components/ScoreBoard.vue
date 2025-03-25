

<template>

    <div>
        ScoreBoard component
    </div>

        <section class="score">
                Player <span>{{this.playerCount}}</span> x <span>{{ this.loseCount }}</span> Computer
        </section>


</template>





<script>

        export default{
                //props sao prorpriedade de dados e nao podemos alterar elas nesse nivel
                props: [ 'playerCount', 'loseCount']
        }   

</script>





<style lang="scss">

    section.score{
        border-bottom: 1px solid black;
        padding: 24px;
        font-size: 18px;
    }

    section.score span{
        padding: 8px;
        font-weight: bold;
        border: 1px solid black;
    }

</style>