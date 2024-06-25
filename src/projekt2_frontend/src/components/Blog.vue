<template>
    <div>
        <button @click="pobierzWpisy">Refresh</button>
        Blog
        {{ wpisy }}
        <input v-model="nowyBlog" type="text"/>
        <button @click="dodajWpis">Dodaj</button>
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
            }
        },
    }
</script>
