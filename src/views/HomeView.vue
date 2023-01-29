<script setup>
import { RouterLink, RouterView } from 'vue-router'
import {ref, computed} from 'vue'
import q from '../data/quizes.json'
import QuizPreview from '../components/QuizPreview.vue';
const quizes = ref(q)

const search = ref('')

//filter quizes by search input
const filteredQuizes = computed(() => {
  return quizes.value.filter(quiz => quiz.header.toLowerCase().includes(search.value.toLowerCase()))
})



</script>

<template>
  <main>
    <header>
      <h1>Welcome to Quizes</h1>
      <input  placeholder="search" v-model="search"/>
    </header>
    <ul>
      <li v-for="quiz in filteredQuizes" :key="quiz.id">
        <RouterLink :to="'/quiz/' + quiz.id">
        <QuizPreview :header="quiz.header" img="{{ quiz.img }}" :nQuestions=quiz.questions.length />
        </RouterLink>
      </li>
    </ul>
</main>
</template>


<style scoped>




header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1em;
  background-color: rgb(31, 31, 31);
  color: white;
  box-shadow: 0 0 10px 0 rgba(0,0,0,0.2);
  margin: 1em;
  border-radius: 10px;
}

input{
  padding: 0.5em;
  margin-right: 3em;
  border: none;
  border-radius: 10px;
  outline: none;
}


ul{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 1em;
  margin: 0 auto;
  padding: 0;

}

li{
  list-style: none;
  text-align: center;
  padding: 0.5em;
  width: 100%;

  /* border: 1px solid black; */
  /* border-radius: 10px; */
  background-color: rgb(31, 31, 31);
  box-shadow: 0 0 10px 0 rgba(0,0,0,0.2);
  
}

</style>