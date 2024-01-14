<script setup lang="ts">
const props = defineProps({
    error: Object
})

const handleError = () => clearError({ redirect: '/' })
</script>

<template>
    <div>
        <h2>{{ error.statusCode }}</h2>
        <button class="text-decoration-underline" @click="handleError">Back to Homepage</button>
    </div>
</template>