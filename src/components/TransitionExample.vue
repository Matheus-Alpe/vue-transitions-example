<template>
    <div class="item">
        <h3 class="d-inline-block title">{{ capitalizeName }}</h3>
        <button class="btn btn-primary btn-sm mb-3" @click="mostrar = !mostrar">Alternar</button>
    
        <transition :name="animationName" type="animation"> 
            <div class="alert alert-primary" v-if="mostrar">v-if - Animações no Vue</div>
        </transition>
        <hr>
    </div>
</template>

<script>
export default {
    props: {
        animationName: String
    },

    data() {
        return {
            mostrar: false
        }
    },

    computed: {
        capitalizeName() {
            return `${this.animationName[0].toUpperCase() + this.animationName.substring(1)}: `
        }
    }
}
</script>


<style>
:root {
    --transition-duration: .5s;
}

.title {
    white-space: pre;
}

/* <fade> */
.fade-enter,
.fade-leave-to {
    opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity var(--transition-duration);
}
/* </fade> */

/* <zoom> */
.zoom-enter,
.zoom-leave-to {
    transform: scale(0);
}

.zoom-enter-active,
.zoom-leave-active {
    transition: transform var(--transition-duration);
}
/* </zoom> */

/* <slide-transition> */
.slide-transition-enter,
.slide-transition-leave-to {
    transform: translateX(-100px);
}

.slide-transition-enter-active,
.slide-transition-leave-active {
    transition: transform var(--transition-duration);
}
/* </slide-transition> */

/* <slide-animation> */
.slide-animation-enter,
.slide-animation-leave-to {
    opacity: 0;
}

.slide-animation-enter-active {
    animation: slide var(--transition-duration);
    transition: opacity var(--transition-duration);
}

.slide-animation-leave-active {
    animation: slide var(--transition-duration) reverse;
    transition: opacity 2s;
}

@keyframes slide {
    /* from {}
    to {} */
    0% {
        transform: translateX(100px);
    }

    100% {
        transform: translateX(0);
    }
}
/* </slide-animation> */
</style>