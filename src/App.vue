<template>
  <div id="app" class="ui container">
    <quiz-list v-bind:quizzes="quizzes" v-on:change-state="changeState"></quiz-list>
    <create-quiz v-show="viewState === 'quizzes'" v-on:create-quiz="createQuiz"></create-quiz>
    <create-flash-card v-show="viewState === 'cards'" v-on:create-flash-card="createFlashCard"></create-flash-card>
  </div>
</template>

<script>

import QuizList from './components/QuizList'
import CreateQuiz from './components/CreateQuiz'
import CreateFlashCard from './components/CreateFlashCard'

export default {
  name: 'app',
  components: {
    QuizList,
    CreateQuiz,
    CreateFlashCard
  },
  methods: {
    createQuiz (newQuiz) {
      const maxId = Math.max.apply(Math, this.quizzes.map(function (q) { return q.id }))
      const nextId = maxId + 1
      this.quizzes.push({
        id: nextId,
        title: newQuiz.title,
        description: newQuiz.title,
        cards: []
      })
    },
    changeState (state) {
      this.viewState = state.viewState
      this.activeQuiz = state.activeQuiz
    },
    createFlashCard (newCard) {
      var id = this.activeQuiz
      // eslint-disable-next-line
      var quizzes = $.grep(this.quizzes, function (e) { return e.id === id })
      if (quizzes.length === 0) return
      const quiz = quizzes[0]
      const maxId = Math.max.apply(Math, quiz.cards.map(function (q) { return q.id }))
      const nextId = maxId + 1
      quiz.cards.push({
        id: nextId,
        term: newCard.term,
        definition: newCard.definition
      })
    }
  },
  data () {
    return {
      quizzes: [
        {
          id: 1,
          title: 'Chapter 1 Example',
          description: 'This is a single example description.',
          cards: [
            {
              id: 1,
              term: 'Some Term 1',
              definition: 'Some definition'
            },
            {
              id: 2,
              term: 'Some Term 2',
              definition: 'Some definition of term 2'
            }
          ]
        }
      ],
      viewState: 'quizzes',
      activeQuiz: 0
    }
  }
}
</script>

<style>
#app {
  
  margin-top: 60px;
}
</style>
