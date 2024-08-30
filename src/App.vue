<script setup>
import axios from 'axios';
import { ref } from 'vue';

const axiosInstance = axios.create({
    baseURL: import.meta.env.VITE_API_ENDPOINT,
});

const input = ref(0)
const matches = ref([]);
const matchForValue = ref('');
const responseCombinations = ref([]);

function getMatches(){

    matchForValue.value = '';

    axiosInstance.get('/api/get-match', {
        'params': {'value': input.value}
    }).then(response => {

        responseCombinations.value = [];
        matchForValue.value = input.value;

        response.data.forEach((item) => {
            responseCombinations.value.push(item);
            matches.value.unshift(item);
        });

        response_modal.showModal()
    })
    .catch(error => {
        console.error('There was an error!', error);
    });
}
</script>

<template>
    <div class="h-full mt-28 max-w-3xl mx-auto font-sans text-4xl">

        <dialog id="response_modal" class="modal">
            <div class="modal-box">
                <h3 v-if="responseCombinations.length" class="text-lg font-bold mb-6">Found matches for input {{matchForValue}}²</h3>
                <h3 v-else class="text-lg font-bold mb-6">No matches found for input {{matchForValue}}²</h3>

                <div v-for="responseCombination in responseCombinations">
                    {{ `${responseCombination.a}² + ${responseCombination.b}² = ${responseCombination.c}²` }}
                </div>
                <div class="modal-action">
                    <form method="dialog">
                        <button class="btn">Okay</button>
                    </form>
                </div>
            </div>
        </dialog>

        <div class="space-y-2">
            <form @submit.prevent="getMatches" class="flex gap-1">
                <input required type="number" class="input input-bordered w-full max-w-xs" v-model="input" />

                <input type="submit" value="List Matches" class="btn">
            </form>
            <hr>
            <table class="table table-md font-mono w-1/2">
                <thead>
                <tr>
                    <th>A² + B² = C²</th>
                    <th>AVG</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="match in matches">
                    <td>{{ `${match.a}² + ${match.b}² = ${match.c}²` }}</td>
                    <td>{{ match.avg }}</td>
                </tr>
                </tbody>
            </table>
        </div>

    </div>
</template>

<style scoped>

</style>
