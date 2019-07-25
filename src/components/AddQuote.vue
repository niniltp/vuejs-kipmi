<template>
    <form class="form-addQuote">
        <input type="text" placeholder="Title" v-model="newQuote.title"
               @keyup.enter="addQuote(newQuote)">
        <input type="text" placeholder="Author" v-model="newQuote.author"
               @keyup.enter="addQuote(newQuote)">
        <input type="text" placeholder="From" v-model="newQuote.from"
               @keyup.enter="addQuote(newQuote)">
        <textarea v-model="newQuote.content" @keydown.enter.exact.prevent
                  @keydown.enter.shift.exact="newline" @keyup.enter="addQuote(newQuote)" rows="3"
                  placeholder="Write something to remember" spellcheck="true"></textarea>
        <SearchbarAutocomplete v-bind:placeholder="'Add some tags'" v-bind:items="tags"
                               v-on:addTagToNewQuote="addTagToNewQuote"></SearchbarAutocomplete>
        <p class="tags">
            Tags:
            <Tag v-for="(newQuoteTag, newQuoteTagIndex) in newQuote.tags" :key="newQuoteTagIndex"
                 v-bind:name="newQuoteTag" v-on:removeTag="removeTagToNewQuote(newQuoteTag)" class="tag"
                 type="button"></Tag>
        </p>
    </form>
</template>

<script>
    import SearchbarAutocomplete from './SearchbarAutocomplete.vue'
    import Tag from './Tag.vue'

    export default {
        name: "AddQuote",
        components: {
            SearchbarAutocomplete,
            Tag
        },
        props: ['tags'],
        data() {
            return {
                newQuote: {
                    title: '',
                    author: '',
                    from: '',
                    content: '',
                    tags: []
                },
            }
        },
        methods: {
            addQuote(newQuote) {
                if (newQuote.content !== '') {
                    const quote = {
                        hover: false,
                        title: this.newQuote.title,
                        author: this.newQuote.author,
                        from: this.newQuote.from,
                        content: this.newQuote.content,
                        tags: this.newQuote.tags
                    };

                    this.$emit('addQuote', quote);

                    this.newQuote = {
                        title: '',
                        author: '',
                        from: '',
                        content: '',
                        tags: []
                    }

                } else this.$emit('showNotifErrorAddQuote');
            },
            addTagToNewQuote(tag) {
                // if the new quote doesn't already have this tag
                if (!this.newQuote.tags.includes(tag)) {
                    // if the tag doesn't exist in the tags list
                    if (!this.tags.includes(tag)) {
                        // create the new tag
                        this.$emit('addTag', tag);
                    }
                    this.newQuote.tags.push(tag);
                }
            },
            removeTagToNewQuote(tag) {
                this.newQuote.tags = this.newQuote.tags.filter(i => i !== tag)
            }
        }
    }
</script>

<style scoped>
    .form-addQuote {
        background: #323333;
    }

    .tags {
        padding: 20px;
        text-align: left;
        font-style: italic;
        color: #a0adb7;
        margin-bottom: 0;
    }

</style>