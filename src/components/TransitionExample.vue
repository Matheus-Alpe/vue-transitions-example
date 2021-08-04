<template>
    <div class="item">
        <h3 class="d-inline-block title">{{ capitalizeName }}</h3>
        <button class="btn btn-primary btn-sm mb-3" @click="mostrar = !mostrar">Alternar</button>
    
        <transition v-if="customCss"
            enter-class=""
            enter-active-class="animate__animated animate__bounceInLeft"
            enter-to-class=""
            
            leave-class=""
            leave-active-class="animate__animated animate__bounceOutDown"
            leave-to-class=""
        >
            <div 
                class="alert alert-primary" 
                v-if="mostrar"
            >v-if - Animações no Vue</div>
        </transition>
        <transition v-else-if="customJs"
            @before-enter="beforeEnter"
            @enter="enter"
            @after-enter="afterEnter"
            @enter-cancelled="enterCancelled"

            @before-leave="beforeLeave"
            @leave="leave"
            @after-leave="afterLeave"
            @leave-cancelled="leaveCancelled"
        >
            <div 
                class="alert alert-primary" 
                v-if="mostrar"
            >v-if - Animações no Vue</div>
        </transition>
        <!-- <transition :name="transitionName" :type="transitionType" :duration="{ enter: 1200, leave: 500 }">  -->
        <transition v-else :name="transitionName" :type="transitionType" > 
            <div 
                class="alert alert-primary" 
                v-if="mostrar"
            >
                v-if - Animações no Vue
            </div>
        </transition>
        <hr>
    </div>
</template>

<script>
export default {
    props: {
        customCss: Boolean,
        customJs: Boolean,
        transitionName: String,
        transitionType: String,
    },

    data() {
        return {
            mostrar: false
        }
    },

    computed: {
        capitalizeName() {
            return `${this.transitionName[0].toUpperCase() + this.transitionName.substring(1)}: `
        }
    },

    methods: {
        beforeEnter(element) {
            console.log('beforeEnter', element)
        },
        enter(element, done) {
            console.log('enter', element)
            done()
        },
        afterEnter(element) {
            console.log('afterEnter', element)
        },
        enterCancelled(element) {
            console.log('enterCancelled', element)
        },
        beforeLeave(element) {
            console.log('beforeLeave', element)
        },
        leave(element, done) {
            console.log('leave', element)
            done()
        },
        afterLeave(element) {
            console.log('afterLeave', element)
        },
        leaveCancelled(element) {
            console.log('leaveCancelled', element)
        },
    }
}
</script>

<style>
:root {
    --transition-duration: .7s;
}

body {
    overflow: hidden;
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
    animation: slide var(--transition-duration) cubic-bezier(.72,-0.03,.78,1.07);
    transition: opacity var(--transition-duration) cubic-bezier(.72,-0.03,.78,1.07);
}

.slide-animation-leave-active {
    animation: slide var(--transition-duration) reverse;
    transition: opacity var(--transition-duration);
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