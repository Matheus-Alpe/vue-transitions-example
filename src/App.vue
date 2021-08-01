<template>
    <div id="app">
        <div class="jumbotron jumbotron-fluid">
            <div class="container">
                <h1 class="display-4">Animações no Vue</h1>
                <p class="lead">Treinando transição/animação de elementos/components no Vue.</p>
            </div>
        </div>

        <div class="container">
            <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">Alternar</button>
            
            <transition name="fade"> 
                <div class="alert alert-primary" v-if="mostrar">v-if - Animações no Vue</div>
            </transition>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            mostrar: true
        }
    }
}
</script>

<style scoped>

/* Transition In & Out*/
.fade-enter,
.fade-leave-to {
    opacity: 0;
}
.fade-enter-active,
.fade-leave-active {
    transition: opacity 1s;
}

.fade-enter-to,
.fade-leave {
    opacity: 1;
}
</style>