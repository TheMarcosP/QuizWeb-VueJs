<script setup>
import { ref, computed } from 'vue';
import { defineEmits } from 'vue';

const emit = defineEmits(['selectOption']);

defineProps({
    question: {
        type: Object,
        required: true
    }
})

const sOp = (isCorrect) => {
    emit("selectOption", isCorrect);
}

</script>

<template>
    <div>
        <h2>{{ question.header }}</h2>
        <ul>
            <li v-for="answer in question.options" :key="answer.id" @click="sOp(answer.isCorrect)">
                {{ answer.text }} {{ answer.isCorrect }}
            </li>
        </ul>

    </div>


</template>


<style>
li{
    list-style: none;
}
</style>