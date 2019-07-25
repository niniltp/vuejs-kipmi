<template>
    <div class="autocomplete">
        <input type="text" v-bind:placeholder="placeholder" v-model="search" @click="isOpen = !isOpen" @keyup.enter="setResult(search)" @input="onChange"/>
        <ul class="autocomplete-results" v-show="isOpen">
            <li class="autocomplete-result" v-for="(result, index) in results" :key="index" @click="setResult(result)">{{result}}</li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'autocomplete',
        props: ['placeholder', 'items'],
        data () {
            return {
                search: '',
                results: this.items.sort(),
                isOpen: false
            }
        },
        methods: {
            onChange() {
                this.results.sort();
                this.isOpen = true;
                this.filterResults();
            },
            filterResults() {
                this.results = this.items.filter(item => item.indexOf(this.search) > -1)
            },
            setResult(result) {
                this.$emit('addTagToNewQuote', result);
                this.search = '';
                this.results = this.items;
                this.isOpen = false;
                this.results.sort();
            }
        }
    }
</script>

<style scoped>
    .autocomplete-results {
        padding: 0 0 5px;
        margin: 0;
        height: auto;
        color: #a0adb7;
        border: none;
    }

    .autocomplete-result {
        list-style: none;
        text-align: left;
        font-size: 1.1em;
        padding: 4px 20px;
        cursor: pointer;
    }

    .autocomplete-result:hover {
        background-color: #3E5252;
    }
</style>