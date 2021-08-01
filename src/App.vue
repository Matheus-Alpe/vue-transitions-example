<template>
    <div id="app">
        <div class="jumbotron jumbotron-fluid">
            <div class="container">
                <h1 class="display-4">Animações no Vue</h1>
                <p class="lead">Treinando transição/animação de elementos/components no Vue.</p>
            </div>
        </div>

        <div class="container">
            <TransitionExample animation-name="fade"/>
            <TransitionExample animation-name="zoom"/>
            <TransitionExample animation-name="slide-transition"/>
            <TransitionExample animation-name="slide-animation"/>
        </div>
    </div>
</template>

<script>
import TransitionExample from './components/TransitionExample.vue'

export default {
    components: {
        TransitionExample
    },
}
</script>