<template>
    <div class="item">

        <h3 class="font-weight-light">Tecnologias</h3>

        <div class="form-group">
            <input 
                type="text" 
                class="form-control" 
                placeholder="Insira um novo item e pressione Enter"
                @keyup.enter="adicionar"
                ref="inputItem">
        </div>

        <transition-group>

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

    </div>
</template>

<script>
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
            this.$refs.value = ''
        },

        remover(indice) {
            this.tecnologias.splice(indice, 1)
        }
    }
}
</script>

<style>

</style>