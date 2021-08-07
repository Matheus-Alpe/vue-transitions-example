<template>
    <div class="item">
        <h3 class="d-inline-block title">{{ capitalizeName }}</h3>
        <button v-if="!select" class="btn btn-primary btn-sm mb-3" @click="mostrar = !mostrar">Alternar</button>
    
        <div v-if="select">
            <div class="form-group">
                <label>Animações:</label>
                <select class="form-control" v-model="animaticaoSelecionada">
                    <option value="fade">Fade</option>
                    <option value="zoom">Zoom</option>
                    <option value="slide-transition">Slide Transition</option>
                    <option value="slide-animation">Slide Animation</option>
                </select>
            </div>
            <div class="form-group">
                <label>Mensagem:</label>
                <select class="form-control" v-model="alertaAtual">
                    <option value="info">Informação</option>
                    <option value="warning">Warning</option>
                    <option value="success">Sucesso</option>
                </select>
            </div>
            <!-- <transition :name="animaticaoSelecionada" appear mode="in-out">  -->
            <transition :name="animaticaoSelecionada" appear mode="out-in"> 
                <div :class="classesAlerta" :key="alertaAtual">Animações no Vue</div>
            </transition>
        </div>

        <transition v-else-if="customCss"

            appear
            appear-class=""
            appear-active-class="animate__animated animate__flipInY"
            appear-to-class=""

            @before-appear="beforeAppear"
            @appear="appear"
            @after-appear="afterAppear"
            @appear-cancelled="appearCancelled"

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
            appear
            @before-enter="beforeEnter"
            @enter="enter"
            @after-enter="afterEnter"
            @enter-cancelled="enterCancelled"

            @before-leave="beforeLeave"
            @leave="leave"
            @after-leave="afterLeave"
            @leave-cancelled="leaveCancelled"

            :css="false"
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
        select: Boolean,
        customCss: Boolean,
        customJs: Boolean,
        transitionName: String,
        transitionType: String,
    },

    data() {
        return {
            mostrar: this.customJs || this.customCss,
            animaticaoSelecionada: 'fade',
            alertaAtual: 'info'
        }
    },

    computed: {
        capitalizeName() {
            return `${this.transitionName[0].toUpperCase() + this.transitionName.substring(1)}: `
        },

        classesAlerta() {
            return {
                'alert': true, 
                [`alert-${this.alertaAtual}`]: true
            }
        }
    },

    methods: {
        beforeAppear(element) {
            console.log('beforeAppear', element)
        },

        appear(element, done) {
            console.log('appear', element)
            done()
        },

        afterAppear(element) {
            console.log('afterAppear', element)
        },

        appearCancelled(element) {
            console.log('appearCancelled', element)
        },

        beforeEnter(element) {
            console.log('beforeEnter')
            element.style.opacity = 0
        },

        enter(element, done) {
            console.log('enter')

            let contagem = 0
            const intervalo = setInterval(() => {
                element.style.opacity = +element.style.opacity + 0.1
                contagem++

                if (contagem > 10) {
                    clearInterval(intervalo)
                    done()
                }

            }, 150)
        },

        afterEnter(element) {
            console.log('afterEnter', element)
        },

        enterCancelled(element) {
            console.log('enterCancelled', element)
        },

        beforeLeave(element) {
            console.log('beforeLeave')
            element.style.transition = 'width .1s'
            element.style.overflow = 'hidden'
            element.style.whiteSpace = 'nowrap'
        },

        leave(element, done) {
            console.log('leave')

            let contagem = 0
            const tamanho = element.offsetWidth

            const intervalo = setInterval(() => {
                element.style.width = (tamanho * (1 - (contagem / 10))) + 'px'
                contagem++

                if(contagem > 10) {
                    clearInterval(intervalo)
                    done()
                }
            }, 150)
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