<script>

//not sure the store goes here
import Vue from 'vue'
    import Vuex from 'vuex'

import _ from 'lodash'

    Vue.use(Vuex)

export default new Vuex.Store({
    state: {
        Question: [],
        current: 0,
        difficultyLevel: null,
        shuffledAnswers: [],
        selectedIndex: null,
        correctIndex: null,
        correctAnswers: 0,
        answered: false,

    }, 
    mutations: {
        SET_DIFFICULTY (state, difficulty) {
            state.difficultyLevel = difficulty
        },
        SET_QUESTION (state, data) {
            state.Question = data
        },
        SHUFFLED_ANSWER(state) {
            var Options;
            Options = _.concat(
                state.Question[state.current].incorrect_answers,
                state.Question[state.current].correct_answer
            );
            state.shuffledAnswers = _.shuffle(Options);
            console.log(state.shuffledAnswers);
        }
    }, 
    actions: {
        beginQuiz:  ({ commit, state }, difficulty) => {
            commit('SET_DIFFICULTY', difficulty)
            fetch(`https://opentdb.comp/api.php?amount=10&category=31&difficulty=${state.difficultyLevel}&type=multiple`)
                .then(response => response.json())
                .then(data=> {
                    commit('SET_QUESTION', data.results)
                    commit ('STOP_LOADING')
                    commit('SHUFFLED_ANSWER')
                    commit('RESETQUIZ')
                    console.log(state.Question)
                })
                .catch(error => console.log("Error: ", error))
        }
    },
})

</script>

