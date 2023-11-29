<script setup>
    const { data: ambientes } = await useFetch('http://localhost:8000/ambientes');

    let showForm = false;
    const setShowForm = () => {
        showForm = true;
        refreshNuxtData()
    }   

    let nomeAmbiente;

    const saveAmbience = async () => {
        console.log("nomeAmbiente", nomeAmbiente);

       await useFetch('http://localhost:8000/ambientes/',{
            method: 'POST',
            body: JSON.stringify([{ nome: nomeAmbiente }]),
            key: 'AmbiencePost'            
        });

        alert("Ambiente Salvo!");
    }

</script>

<template>
    <div>
        <h1>Ambientes:</h1>
        <section v-for="ambiente in ambientes.data" :key="ambiente.id">
            <h3>{{ ambiente.nome }}</h3>
        </section>

        <button @click="setShowForm">Cadastre um novo ambiente!</button>

        <br><br>

        <section v-if="showForm === true">
            <div>
                <label for="">Qual o Nome do Ambiente?</label> <input type="text" v-model="nomeAmbiente">
            </div>

            <br>

            <button @click="saveAmbience">cadastrar Ambiente</button>
        </section>
        
    </div>
</template>