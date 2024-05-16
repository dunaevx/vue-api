<template>
    <div class="app">
        <div class="filters">
            <input v-model="filters.name" placeholder="Filter by name" />
            <select v-model="filters.status">
                <option value="">Filter by status</option>
                <option value="alive">Alive</option>
                <option value="dead">Dead</option>
                <option value="unknown">Unknown</option>
            </select>
            <button @click="onFilters">Apply</button>
        </div>
        <div class="wrapper">
            <Card v-for="(el, index) in characters" :key="index" :card="el" />
        </div>
        <div class="pagination">
            <button @click="prevPage" :disabled="page === 1">Previous</button>
            <span>Page {{ page }}</span>
            <button @click="nextPage" :disabled="!hasMore">Next</button>
        </div>
    </div>
</template>

<script>
import { ref, onMounted, watch } from 'vue';
import axios from 'axios';
import Card from './components/Card.vue';

export default {
    components: { Card },
    setup() {
        const characters = ref([]);
        const page = ref(1);
        const hasMore = ref(true);
        const filters = ref({
            name: '',
            status: ''
        });

        const fetchCharacters = async () => {
            try {
                const response = await axios.get('https://rickandmortyapi.com/api/character', {
                    params: {
                        page: page.value,
                        name: filters.value.name,
                        status: filters.value.status
                    }
                });
                characters.value = response.data.results;
                hasMore.value = response.data.info.next !== null;
            } catch (error) {
                console.error(error);
            }
        };

        const onFilters = () => {
            page.value = 1;
            fetchCharacters();
        };

        const prevPage = () => {
            if (page.value > 1) {
                page.value--;
                fetchCharacters();
            }
        };

        const nextPage = () => {
            if (hasMore.value) {
                page.value++;
                fetchCharacters();
            }
        };

        onMounted(fetchCharacters);

        watch(filters, onFilters);

        return { characters, page, hasMore, filters, onFilters, prevPage, nextPage };
    }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.app {
    font-family: 'Roboto', sans-serif;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.filters {
    margin-bottom: 20px;
}

.filters input, .filters select, .filters button {
    padding: 10px;
    margin: 5px;
}

.wrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.pagination {
    margin-top: 20px;
}



.pagination button {
    padding: 10px 20px;
    margin: 5px;
}

.pagination span {
    padding: 10px;
    margin: 5px;
}
</style>
