<template>
    <div class="quote">
        <blockquote class="blockquote">
            <div class="text">
                <h3 v-if="quote.title !== ''">{{quote.title}}</h3>
                <p><q>{{quote.content}}</q></p>
                <footer class="blockquote-footer">
                    <span v-if="quote.author === ''">Unknown</span><span v-else>{{quote.author}}</span>
                    <span v-if="quote.from !== ''">, from <cite>{{quote.from}}</cite></span>
                    <p class="tags" v-if="quote.tags.length > 0">Tags: <span v-for="(tag, index) in quote.tags" :key="index"><a href="#">{{tag}}</a><span v-if="index !== quote.tags.length - 1">, </span></span></p>
                </footer>
            </div>
            <i v-if="quote.hover == true" class="fa fa-minus-circle fa-2x destroy" @click="$emit('removeQuote', quote)"></i>
        </blockquote>
    </div>
</template>

<script>
    export default {
        name: 'quotes',
        props: ['quote']
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

    h3 {
        text-align: center;
        font-weight: bold;
        padding: 30px 0 50px;
    }

    h3::first-letter {
        text-transform: uppercase;
    }

    .quote {
        padding: 10px 0px 20px 0px;
    }

    .text > p > q {
        quotes: '\00AB ' ' \00BB';
        color: gray;
        font-size: 1em;
        font-weight: 400;
    }

    .text > p {
        text-align: justify;
        text-justify: auto;
        white-space: pre-wrap;
    }


    .blockquote {
        border: none;
        padding-bottom: 50px;
    }

    .text {
        width: 90%;
        float: left;
    }

    .blockquote-footer {
        text-align: right;
        font-size: 1em;
    }

    .tags {
        text-align: left;
        font-style: italic;
        font-size: 0.9em;
    }

    .destroy {
        float: right;
        cursor: pointer;
    }


</style>
