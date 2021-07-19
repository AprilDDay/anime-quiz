
<template>
    <div>
        <div class="container">
            <div v-if="Question.length">
                <h1><span>Question: {{current +1}}</span></h1>
                <h2>{{ Question[current].question }}</h2>
                <div class="options">
                    <ul v-for="(options, index) in shuffledAnswers" :key="index">
                        <li @click="selectedAnswer(index)">{{ options }}</li>
                    </ul>
                </div>
                <div class="nav">
                    <button>submit</button>
                    <button @click="next">next</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import {mapState} from 'vuex'

    export default {
        methods: {
            ...mapAction(['next'])
        },
        computed: {
            ...mapState(['Question', 'current']),
        },
        mutations: {
            NEXT (state) {
                state.current++
            },
            SELECTED_ANSWER (state, index) {
                console.log(index)
                state.selectedIndex = index
            },
            SHUFFLE_ANSWER (state) {
                var Options 
                Options = _.concat(state.Question[state.current].incorrect_answers, state.Question[state.current].correct_answer)
                state.shuffledAnswers = _.shuffle(Options)
                state.correctIndex = state.shuffledAnswers.indexOf(state.Question[state.current].correct_answer)
            },
        },
        actions: {
            next: ({commit}) => {
                commit('NEXT')
            }, 
            selectedAnswwer: ({ commit}, index) => {
                commit('SELECTED_ANSWER', index)
            }
        },
        watch: {
            current: {
                handler() {
                    this.$store.commit('SHUFFLE_ANSWER')
                }
            }
        }
    }
</script>