<template>
    <div class="item">

        <h3 class="font-weight-light">Animações de Estado</h3>

        <div class="form-group">
            <input type="number" class="form-control" v-model="numero"
                step="50">
        </div>

        <div class="alert alert-info">
            <h3 class="font-weight-light">
                <strong>Número: </strong>
                <span>{{ numeroAnimado }}</span>
            </h3>
        </div>

        <hr>
    </div>
</template>

<script>
import { TweenLite } from 'gsap/TweenLite'

export default {
    data() {
        return {
            numero: 0,
            numeroInterpolado: 0
        }
    },

    computed: {
        numeroAnimado() {
            return this.numeroInterpolado.toFixed(0)
        }
    },

    watch: {
        numero(novoNumero) {
            TweenLite.to(this.$data, 2, { numeroInterpolado: novoNumero })
        }
    }
}
</script>

<style>

</style>