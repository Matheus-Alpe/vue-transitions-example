<template>
    <div class="item">

        <h3 class="font-weight-light">Tecnologias</h3>

        <div class="row">

            <div class="col-sm-2">
                <button class="btn btn-info" @click="embaralhar">Embaralhar</button>
            </div>

            <div class="col-sm-10">
                <div class="form-group">
                <input 
                    type="text" 
                    class="form-control" 
                    placeholder="Insira um novo item e pressione Enter"
                    @keyup.enter="adicionar"
                    ref="inputItem">
                </div>
            </div>

        </div>

        

        <transition-group tag="ul" class="list-group" name="list">

            <li 
                class="list-group-item"
                v-for="(tecnologia, indice) in tecnologias"
                :key="tecnologia">

                    <span>{{ tecnologia }}</span>
                    <button 
                        class="btn btn-danger btn-sm float-right"
                        @click="remover(indice)">
                            x
                    </button>

            </li>

        </transition-group>

        <hr>
    </div>
</template>

<script>
import { shuffle } from 'lodash'

export default {
    data() {
        return {
            tecnologias: [
                'Javascript',
                'VueJs',
                'Vuex',
                'Vue Router'
            ]
        }
    },

    methods: {
        /**
         * @param { KeyboardEvent } event
         */
        adicionar(event) {
            const novoItem = event.target.value
            if (!novoItem) return
            const indice = Math.floor(Math.random() * this.tecnologias.length)
            this.tecnologias.splice(indice, 0, novoItem)
            this.$refs.inputItem.value = ''
        },

        remover(indice) {
            this.tecnologias.splice(indice, 1)
        },

        embaralhar() {
            this.tecnologias = shuffle(this.tecnologias)
        }
    }
}
</script>

<style>
.list-enter,
.list-leave-to {
    opacity: 0;
    transform: translateX(-70px);
}

.list-enter-active,
.list-leave-active,
.list-move {
    transition: all .5s;
}

.list-leave-active {
    position: absolute;
    width: calc(100% - 100px);
}

</style>