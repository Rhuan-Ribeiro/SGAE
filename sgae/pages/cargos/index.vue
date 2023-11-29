<script setup>
    const { data: cargos } = await useFetch('http://localhost:8000/cargos');
</script>

<template>
    <div>
        <h1>Cargos:</h1>
        <section v-for="cargo in cargos.data" :key="cargo.id">
            <h3>{{ cargo.nome }} - Nivel de acesso: {{ cargo.nivelAcesso }}</h3>
        </section>
    </div>
</template>