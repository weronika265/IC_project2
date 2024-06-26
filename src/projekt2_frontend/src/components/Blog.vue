<template>
    <div>
        <h2 class="text-blue-600">Wpisy na bloga:</h2>
        <div class="w-100 flex flex-row-reverse">
            <button class="bg-blue-600 rounded text-white p-4" @click="pobierzWpisy">Refresh</button>
        </div>
        <div class="grid mx-6 gap-4 my-4">
            <div v-for="(wpis, index) in wpisy" class="drop-shadow-xl bg-stone-300 p-4">
                <p>id: {{ index }}</p>
                <p>{{ wpis }}</p>
                <button class="bg-blue-600 rounded text-white p-4" @click="usunWpis(index)">Usuń</button>
                <!-- <button class="bg-blue-600 rounded text-white p-4" @click="edytujWpis(index)">Edytuj</button> -->
            </div>
        </div>
        <div class="flex justify-center flex-col">
            <input v-model="nowyBlog" class="border-2 border-blue-600 p-4" type="text" />
            <button class="bg-blue-600 rounded text-white p-4" @click="dodajWpis">Dodaj</button>
        </div>
    </div>
</template>

<script>
import { projekt2_backend } from 'declarations/projekt2_backend/index';

export default {
    data() {
        return {
            wpisy: [],
            nowyBlog: ""
        }
    },
    methods: {
        async pobierzWpisy() {
            this.wpisy = await projekt2_backend.odczytaj_wpisy();
        },
        async dodajWpis() {
            await projekt2_backend.dodaj_wpis(this.nowyBlog);
        },
        async usunWpis(index) {
            await projekt2_backend.usun_wpis(index);
            await this.pobierzWpisy();
        },
        // async edytujWpis() {
        //     await projekt2_backend.edytuj_wpis(index, this.nowyBlog);
        // },
    },
    async mounted() {
        this.pobierzWpisy()
    }
}
</script>
