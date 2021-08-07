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
                <span>{{ numero }}</span>
            </h3>
        </div>

        <hr>
    </div>
</template>

<script>
export default {
    data() {
        return {
            numero: 0
        }
    }
}
</script>

<style>

</style>