<template>
    <div class="quotes">
        <ul>
            <transition-group name="list" enter-active-class="animated bounceInUp"
                              leave-active-class="animated bounceOutDown">
                <li v-for="(quote, index) in quotes" :key='index' @mouseover="quote.hover = true"
                    @mouseleave="quote.hover = false">
                    <Quote v-bind:quote="quote" v-on:removeQuote="$emit('removeQuote', quote)"></Quote>
                </li>
            </transition-group>
        </ul>
    </div>
</template>

<script>
    import Quote from './Quote.vue'

    export default {
        name: 'quotes',
        components: {
            Quote
        },
        props: ['quotes', 'tags']
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    ul {
        margin: 0;
        padding: 0;
        list-style-type: none;
    }

    ul li {
        padding: 10px 30px 30px 30px;
        background-color: #E0EDF4;
        border-left: 5px solid #3EB3F6;
        margin-bottom: 2px;
        color: #3E5252;
        display: inline-block;
        width: 100%;
    }

</style>
