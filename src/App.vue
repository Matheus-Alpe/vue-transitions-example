<template>
    <div id="app">
        <div class="jumbotron jumbotron-fluid">
            <div class="container">
                <h1 class="display-4">Animações no Vue</h1>
                <p class="lead">Treinando transição/animação de elementos/components no Vue.</p>
            </div>
        </div>

        <div class="container">
            
            <TransitionState/>
            <TransitionGroup/>
            <TransitionExample select transition-name="select transition"/>
            <TransitionExample transition-name="fade" transition-type="transition"/>
            <TransitionExample transition-name="zoom" transition-type="transition"/>
            <TransitionExample transition-name="slide-transition" transition-type="transition"/>
            <TransitionExample transition-name="slide-animation" transition-type="animation"/>
            <TransitionExample custom-css transition-name="custom-css"/>
            <TransitionExample custom-js transition-name="custom-js"/>
        </div>
        
        <hr>
    </div>
</template>

<script>
import TransitionExample from './components/TransitionExample.vue'
import TransitionGroup from './components/TransitionGroup.vue'
import TransitionState from './components/TransitionState.vue'

export default {
    components: {
        TransitionExample,
        TransitionGroup,
        TransitionState
    },
}
</script>