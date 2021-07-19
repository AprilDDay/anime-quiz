<template>
    <div>
        <header>
            <h1>Anime quiz</h1>
            <div>
                <button @click="$store.commit('RESETQUIZ')>reset</button>
            </div>
        </header>
    </div>
</template>

<script>
    import Vue from 'vue'
    import Vuex from 'vuex'

    Vue.use(Vuex)


//not sure about this vue store
//https://vuex.vuejs.org/guide/#the-simplest-store
    const store = new Vuex.Store({
        state: {
            difficultyLevel: null,
        }, 
        mutations: {

            
        }
    })

</script>
