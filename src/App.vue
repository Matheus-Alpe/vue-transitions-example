<template>
    <div id="app">
        <div class="jumbotron jumbotron-fluid">
            <div class="container">
                <h1 class="display-4">Animações no Vue</h1>
                <p class="lead">Treinando transição/animação de elementos/components no Vue.</p>
            </div>
        </div>

        <div class="container">
            <TransitionExample select transition-name="select transition"/>
            <TransitionExample transition-name="fade" transition-type="transition"/>
            <TransitionExample transition-name="zoom" transition-type="transition"/>
            <TransitionExample transition-name="slide-transition" transition-type="transition"/>
            <TransitionExample transition-name="slide-animation" transition-type="animation"/>
            <TransitionExample custom-css transition-name="custom-css"/>
            <TransitionExample custom-js transition-name="custom-js"/>
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