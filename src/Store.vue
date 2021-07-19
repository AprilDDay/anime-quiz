<script>
import Vue from 'vue'
    import Vuex from 'vuex'

    Vue.use(Vuex)

export default new Vuex.Store({
    state: {
        
        difficultyLevel: null,
    }, 
    mutations: {
        SET_DIFFICULTY (state, difficulty) {
            state.difficultyLevel = difficulty
        }
    }, 
    actions: {
        beginQuiz:  ({commit}, difficulty) => {
            commit('SET_DIFFICULTY', difficulty)
        }
    },
})

</script>

