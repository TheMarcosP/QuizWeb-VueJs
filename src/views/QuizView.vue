<script setup>
    import { useRoute, useRouter } from 'vue-router';
    import { ref, computed } from 'vue';
    import q from '../data/quizes.json';
    import Question from '../components/Question.vue';
    import { RouterLink } from 'vue-router';

    //get the id from the route
    const route = useRoute();
    const id = route.params.id;
    const currentQuestion = ref(0);
    const correctAnswers = ref(0);
    const showResult = ref(false);
    //get quiz
    const quiz = computed(() => {
        return q.find(q => q.id == id);
    });

    const barPercentage = computed(() => {
        return `${currentQuestion.value / quiz.value.questions.length * 100 }%`;
    });

    const selectOption = (isCorrect) => {
        if (isCorrect) {
            correctAnswers.value++;
        }
        currentQuestion.value++;
        if(currentQuestion.value >= quiz.value.questions.length) {
            showResult.value = true;
        }
    }

</script>


<template>
    <header>
        <h2>{{ quiz.header }}</h2>
        <h3> question {{ currentQuestion}}/{{ quiz.questions.length }}</h3>
        {{ barPercentage  }}
        <div class="bar">
            <div class="completion" :style='{width: barPercentage } '></div>
        </div>
    </header>
    <div v-if="!showResult">
        <Question :question="quiz.questions[currentQuestion]" @selectOption="selectOption"/>
    </div>
    <div v-else>
        <h1>Result</h1>
        <h2>You got {{ correctAnswers }} out of {{ quiz.questions.length }} correct</h2>
        <RouterLink to="/">Go back</RouterLink>
    </div>

</template>


<style scoped>

header {
    display: flex;
    flex-direction: column;
    min-width: 500px;
    justify-content: space-between;
    align-items: center;
    padding: 1em;
    background-color: rgb(31, 31, 31);
    color: white;
    box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.2);
    margin: 1em;
    border-radius: 10px;
}

.bar {
    width: 100%;
    height: 20px;
    border-radius: 10px;
    border: 1px solid #e2b714;
}

.completion {
    height: 100%;
    background-color: #e2b714;
    border-radius: 10px;
}

</style>