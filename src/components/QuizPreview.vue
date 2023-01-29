<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    header: {
        type: String,
        required: true
    },
    img: {
        type: String,
        required: true
    },
    nQuestions: {
        type: String,
        required: true
    }
})


</script>

<template>
    <main>
        <div>
            <img :src="'src/data/images/math.webp'" alt="quiz image" />
            <h2>{{ header }}</h2>
            <h3>{{ nQuestions }} questions</h3>
        </div>
        
    </main>
</template>

<style scoped>
img{
    width: 100%;
}

</style>