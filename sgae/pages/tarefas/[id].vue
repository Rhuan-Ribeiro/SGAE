<script setup>
    const route = useRoute();
    const { data: tarefa } = await useFetch(`http://localhost:8000/tarefas/${route.params.id}`);
    const { data: responsaveis } = await useFetch(`http://localhost:8000/tarefasUsuarios?tarefa=${route.params.id}`);
    const { data: statusFound } = await useFetch(`http://localhost:8000/tarefasStatus?tarefa=${route.params.id}`);

</script>

<template>
    <div>
        
        <h1>{{ tarefa.data.nome }}</h1>
        <h3>Status: {{ tarefa.data.idStatusFK.nome }}</h3>
        <h3>Ambiente: {{ tarefa.data.idAmbienteFK.nome }}</h3>
        <h3>Prazo: {{ tarefa.data.prazo }}</h3>
        <h3>Data de Inicio: {{ tarefa.data.dataInicio }}</h3>
        <h3>Data de Fim: {{ tarefa.data.dataFim }}</h3>
        <p>Descrição: {{ tarefa.data.descricao }}</p>
        <h3>Solicitante: {{ tarefa.data.idSolicitanteFK.nome }}</h3>       
        <img :src="tarefa.data.idSolicitanteFK.image" alt="Foto do solicitante">
        
        <h1>Responsáveis:</h1>

        <section v-for="responsavel in responsaveis.data" :key="responsavel.id">
            <h3>Responsavel: {{ responsavel.idUsuarioFK.nome }}</h3>
            <img :src="responsavel.idUsuarioFK.image" alt="Imagem do responsavel">
        </section> 

        <section v-for="status in statusFound.data" :key="status.id">
            <h3>Status: {{ status.idStatusFK.nome }}</h3>
            <h3>Data: {{ status.data }}</h3>
            
        </section> 
  
    </div>
</template>