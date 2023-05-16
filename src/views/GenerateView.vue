<template>
    <div class="generate dark:bg-slate-900 flex sm:justify-center sm:py-8">
        <form class="w-full max-w-sm lg:max-w-full" method="post">
            <div class="flex items-center border-b border-teal-500 py-2">
                <input type="text" required placeholder="Paste your link here"
                class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" aria-label="Generate"
                v-model="payload.destination">

                <select v-model="payload.type" class="text-white bg-teal-500 block appearance-none mx-1.5 border hover:bg-teal-700 px-4 py-2 pr-8 rounded shadow leading-tight focus:outline-none focus:shadow-outline">
                    <option value="public" class="bg-white text-teal-500" selected>Public</option>
                    <option value="private" class="bg-white text-teal-500">Private</option>
                </select>

                <button @click="makeGenerate" class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded" type="button">
                    Generate
                </button>
            </div>

            <div v-if="validate">
                <p v-if="validate.destination">{{ validate.destination[0] }}</p>
            </div>

            <div class="md:flex bg-slate-100 mt-4 rounded-xl p-8 md:p-0 dark:bg-slate-800">
                <div class="pt-6 md:p-8 text-center space-y-4"> 
                    <p class="text-lg font-medium">
                        <span v-if="result.source">Source: {{ result.source }}</span>
                        <br>
                        <span v-if="result.password">Password: {{ result.password }}</span>
                    </p>
                </div>
            </div>
           
        </form>
        
    </div>
    <footer class="md:flex md:items-center md:justify-between md:p-6 dark:bg-gray-800">
        <span  class="text-sm text-gray-500 sm:text-center dark:text-gray-400">Made by <a href="https://arifnofriadi.netlify.app" target="_blanks">xdev</a></span>
    </footer>
</template>


<script setup>
   import axios from 'axios';
   import { reactive, ref } from 'vue';

//    two way data binding => perubahan data akan di bind pada bagian template akan diperbarui


    const validate = ref(null);

    //    variable reactivity
    const payload = ref({
        destination: '',
        type       : 'public',
    });

    const result = reactive({
        source: null,
        password: null,
    });


    //    composision api 
    async function makeGenerate() {
        try{
            const response = await axios({
            method: 'post',
            url: 'https://fetchapi-url-shortener.vercel.app/generate',
            headers: {
                'Content-Type': 'application/json'
            },
            data: {
                'destination': payload.value.destination,
                'type'       : payload.value.type.toUpperCase(),
            }
        })

        result.source = response.data.data.source
        result.password = response.data.data.password
        }catch(e){
            validate.value = e.response.data;
        }
       
    }


</script>

<style>
@media (min-width: 1024px) {
  .generate {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>