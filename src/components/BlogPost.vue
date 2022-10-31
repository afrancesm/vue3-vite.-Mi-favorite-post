<script setup>

defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: 'Sin descripción'
    }
})

const emit = defineEmits(['cambiarFavoritoProp']);


</script>

<template>
    <div class="col">
        <div class="card text-dark mb-3 h-100">
            <div class="card-body">
                <h5 class="card-title">{{ id }} - {{ title }}</h5>
                <p>{{ body }}</p>
                <button class="btn btn-outline-primary"
                @click="emit('cambiarFavoritoProp', title)">Favorito</button>
            </div>
        </div>
    </div>

</template>