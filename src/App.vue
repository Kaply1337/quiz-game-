<script setup>
import { ref , computed } from 'vue'

    const questions = ref([
        {
            question: 'Что такое Vue Js',
            answer: 0,
            options: [
                'Это фреймворк',
                'Это библиотека',
                'Это марка мороженого',
            ],
            selected: null
        },
        {
            question: 'Что такое Vuex?',
            answer: 2,
            options: [
                'Это компонент Vue Js',
                'Это фирма молока ',
                'Библиотека управления проектом'
            ],
            selected: null
        },
        {
            question: 'Для чего используется Vue Router?',
            answer: 1,
            options: [
                'Прогулка по космосу',
                'Библиотека маршутизации для Vue Js',
                'Соус для пиццы',
                'Викторины'
            ],
            selected: null
        },
        {
            question: 'Что такое реактивность во Vue Js?',
            answer: 2,
            options: [
                'Позволяет собирать реакторы проекта',
                'Ракета созданная в СССР',
                'Адаптироваие интерфейса под изминение данных',
                'Сборка проекта занимающие короткое время'
            ],
            selected: null
        },
        {
            question: 'Что такое Composition API в Vue3',
            answer: 3,
            options: [
                'Позволяет добавлять v-model сколько желателе',
                'Нововидение , позволяющие сохранять данные в облоке',
                'Инструмент для запуска веб-проекта на сервере',
                'Нововидение, позволяющие хранить данные отдельно от компонентов'
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
        question.index = currentQuestion.value
        return question
})

    const SetAnswer = evt => {
        questions.value[currentQuestion.value].selected = evt.target.value
        evt.target.value = null
    }

    const NextQuestion = () => {
        if (currentQuestion.value <  questions.value.length - 1) {
            currentQuestion.value++
        } else {
            quizCompleted.value = true
        }
    }

</script>

<template>

<main class="app">
    <h1>The Quiz</h1>

    <section class="quiz" v-if="!quizCompleted">
        <div class="quiz-info">
            <span class="question"> {{ getCurrentQuestion.question }} </span>
            <span class="score">Score {{ score }} / {{ questions.length }}</span>
        </div>

        <div class="options">
            <label v-for="(option, index) in getCurrentQuestion.options" :key="index" :class="`option ${
                        getCurrentQuestion.selected == index
                        ? index === getCurrentQuestion.answer
                        ? `correct`
                        : 'wrong'
                        : ''
                     } ${
                        getCurrentQuestion.selected != null &&
                        index != getCurrentQuestion.selected
                        ? 'disabled'
                        : ''
                     }`">
                <input
                        type="radio"
                        :name="getCurrentQuestion.index"
                        :value="index"
                        v-model="getCurrentQuestion.selected"
                :disabled="getCurrentQuestion.selected"
                @change="SetAnswer">
                <span> {{ option}}</span>
            </label>
        </div>

        <button
        @click="NextQuestion"
        :disabled="!getCurrentQuestion.selected">
            {{
            getCurrentQuestion.index == questions.length - 1
            ? 'Finish'
            : getCurrentQuestion.selected == null
            ? 'Select an option'
            : 'Next is selection'
            }}

        </button>
    </section>
    <section v-else>
      <h2>Вы прошли тест!</h2>
        <p>Ваши баллы {{ score }} / {{ questions.length }}</p>

        <img class="photo" src="../src/assets/happy.jpg" alt="photo">
    </section>
</main>
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
  .app {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 2rem;
      min-height: 100vh;
  }
    h1 {
        font-size: 2rem;
        margin-bottom: 2rem;
    }
    .quiz {
        background-color: #382a4b;
        padding: 1rem;
        width: 100%;
        max-width: 640px;
        border-radius: 0.5rem;
    }
    .quiz-info {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1rem;
    }
    .quiz-info .question {
        color: #8f8f8f;
        font-size: 1.25rem;
    }
    .quiz-info .score {
        font-size: 1.25rem;
        color: #fff;
    }
    .option {
        display: block;
        padding: 1rem;
        background-color: #271c36;
        margin-bottom: 0.5rem;
        border-radius: 0.5rem;
        cursor: pointer;
    }
    .option:hover {
        background-color: #2d213f;
    }

    .option.correct {
        background-color: #2cce7d;
    }
    .option.wrong {
        background-color: #ff5a5f;
    }
    .option:last-of-type {
        margin-bottom: 0;
    }
    .option.disabled {
        opacity: 0.5;
    }
    .option input {
        display: none;
    }
    button {
        appearance: none;
        outline: none;
        border: none;
        cursor: pointer;

        padding: 0.5rem 1rem;
        background-color: #2cce7d;
        color: #2d213f;
        font-weight: 700;
        text-transform: uppercase;
        font-size: 1.25rem;
        border-radius: 0.5rem;
        position: relative;
       top: 0.5rem;

    }
    button:disabled {
        opacity: 0.8;
    }
    h2 {
        font-size: 2rem;
        margin-bottom: 2rem;
        text-align: center;
    }

    p {
        color: #8f8f8f;
        font-size: 1.25rem;
    }
    .photo {
        width: 500px;
        height: 300px;
    }
</style>
