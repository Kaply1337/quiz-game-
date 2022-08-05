<script setup>
import { ref , computed } from 'vue'

    const questions = ref([
        {
            question: 'What is Vue JS?',
            answer: 0,
            options: [
                'A front end framework',
                'A library',
                'An ice cream maker',
            ],
            selected: null
        },
        {
            question: 'What is Vuex?',
            answer: 2,
            options: [
                'Vue with an x',
                'A milk selection',
                'State management library'
            ],
            selected: null
        },
        {
            question: 'What is Vue Router used for?',
            answer: 1,
            options: [
                'Walking to space',
                'A routing library for Vue JS',
                'Pizze sause',
                'Quizzes'
            ],
            selected: null
        }
    ])

    const quizCompleted = ref(false);
    const currentQuestion = ref(0);
    const score = computed(() => {
        let value = 0;
        questions.value.map(q => {
            if (q.selected == q.answer) {
                value++
            }
        })
        return value
    })

    const getCurrentQuestion = computed(() => {
        let question = questions.value[currentQuestion.value]
})

</script>

<template>
<H1>Hello, world</H1>
</template>

<style>
  * {
    margin:0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Montserrat', sans-serif;
  }
  body {
    background-color: #271c36;
    color: #FFF;
  }
</style>
