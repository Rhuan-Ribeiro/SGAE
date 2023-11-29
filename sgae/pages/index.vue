<script setup>
    const route = useRoute();

    const {data: userFound} = 
    await useFetch(`http://localhost:8000/usuarios/`,{
        key: 'userRequest'
    });

    definePageMeta({
        layout: 'empty'
    });

    const verify = async () => {
        refreshNuxtData();
    }
</script>

<template>
    <div>
        <h1 class="title">Bem-vindo ao Sistema!</h1>
        <!-- <font-awesome-icon :icon="['fas', 'graduation-cap']" /> -->

            <label for="">Email:</label> 
            <select v-model="emails">
                <option v-for="user in userFound.data" :key="user.id" :value="user.email"> 
                    {{ user.email }}
                </option>                    
            </select>

            <br>
            <br>

            <div class="emails">
                <button @click="verify">Verificar</button>

                <section v-if="emails != null">
                    <NuxtLink to="/home/">
                        <button>Login</button>
                    </NuxtLink>
                </section>
            </div>
            
            
    </div>
</template>

<style scoped>
    .title {
        color: grey;
        font-size: 24px;
        font-family: Verdana, Tahoma, sans-serif;
    }

    .emails {
        display: flex;
    }
</style>