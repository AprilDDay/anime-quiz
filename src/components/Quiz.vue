
<template>
    <div>
        <div class="container">
            <div v-if="Question.length">
                <h1><span>Question: {{current +1}}</span></h1>
                <h2>{{ Question[current].question }}</h2>
                <div class="options">
                    <ul v-for="(options, index) in shuffledAnswers" :key="index">
                        <li @click="selectedAnswer(index)" :class="checkAnswerClass(index)">{{ options }}</li>
                    </ul>
                </div>
                <div class="nav">
                    <button @click="submit" :disabled="selectedIndex == null || answered">submit</button>
                    <button @click="next" :disabled="answered==false">next</button>
                </div>
                <!-- not sure if thsi looks right here -->
                <div>
                    <h1>Score: <span>{{ correctAnswers }}/{{ Question.length }}</span></h1>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

//the following structure may not be a good one...

    import { mapState, mapActions } from 'vuex'

    export default {
        methods: {
            ...mapActions(['next', 'selectedAnswer', 'submit']),
            checkAnswerClass (index){
                let answerClass = ''
                if (!this.answered && this.selectedIndex === index) {
                    answerClass = 'selected'
                } else if (this.answered && this.correctIndex === index ) {
                    answerClass = 'correctanswer'
                } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index ) {
                    answerClass = 'incorrectanswer'
                }
                return answerClass
            }
        },
        computed: {
            ...mapState(['Question', 'current', 'selectedIndex', 'shuffledAnswers', 'correctIndex', 'answered', 'correctAnswers']),
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
            SUBMIT (state, iscorrect) {
                if(iscorrect){
                    state.correctAnswer++
                }
                state.answered = true
            },
            RESET (state) {
                state.selectedIndex = null
                state.answered = false
            }, 
            RESETQUIZ (state) {
                state.current = 0
                state.corectAnswers = 0
            }
        },
        actions: {
            next: ({commit}) => {
                commit('NEXT')
            }, 
            selectedAnswwer: ({ commit}, index) => {
                commit('SELECTED_ANSWER', index)
            },
            submit: ({ commit, state }) => {
                let iscorrect = false
                if (state.selectedIndex === state.correctIndex) {
                    iscorrect = true
                }
                commit('SUBMIT', iscorrect)
            }
        },
        watch: {
            current: {
                handler() {
                    this.$store.commit('RESET')
                    this.$store.commit('SHUFFLE_ANSWER')
                }
            }
        }
    }
</script>

<style>
    .selected{
        background: skyblue;
    }

    .correctanswer{
        background: springgreen;
    }

    .incorrectanswer{
        background: tomato;
    }

</style>