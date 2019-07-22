<template>
    <div class="container">
        <div class="main">
            <form>
                <input type="text" placeholder="Title" class="newQuote" v-model="newQuote.title"
                       @keyup.enter="addQuote">
                <input type="text" placeholder="Author" class="newQuote" v-model="newQuote.author"
                       @keyup.enter="addQuote">
                <input type="text" placeholder="From" class="newQuote" v-model="newQuote.from"
                       @keyup.enter="addQuote">
                <textarea class="newQuote" v-model="newQuote.content" @keydown.enter.exact.prevent
                          @keydown.enter.shift.exact="newline" @keyup.enter="addQuote" rows="3"
                          placeholder="Write something to remember" spellcheck="true"></textarea>
            </form>
            <div class="quotes">
                <ul>
                    <transition-group name="list" enter-active-class="animated bounceInUp"
                                      leave-active-class="animated bounceOutDown">
                        <li v-for="(quote, index) in quotes" :key='index' @mouseover="quote.hover = true"
                            @mouseleave="quote.hover = false">
                            <Quote v-bind:quote="quote" v-on:removeQuote="removeQuote(quote)"></Quote>
                        </li>
                    </transition-group>
                </ul>
            </div>

            <footer class="footer">
                <p> Keep in mind.</p>
            </footer>
        </div>
    </div>
</template>

<script>
    import Quote from './Quote.vue'

    export default {
        name: 'quotes',
        components: {
            Quote
        },
        data() {
            return {
                quotes: [
                    {
                        hover: false,
                        title: 'quote 1',
                        author: '',
                        from: 'Somewhere',
                        content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed at rhoncus est. Fusce felis sem, dignissim vel felis sit amet, scelerisque tempus orci. Quisque malesuada neque a leo viverra, a pharetra dui maximus. Curabitur nunc purus, porta et nisi ultricies, feugiat gravida velit. Donec ac semper arcu. Nulla lacinia erat sed est condimentum pellentesque. Sed ante libero, pharetra et ultrices non.'
                    },
                    {
                        hover: false,
                        title: 'Quote 2',
                        author: 'Unknown',
                        from: '',
                        content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed at rhoncus est. Fusce felis sem, dignissim vel felis sit amet, scelerisque tempus orci. Quisque malesuada neque a leo viverra, a pharetra dui maximus. Curabitur nunc purus, porta et nisi ultricies, feugiat gravida velit. Donec ac semper arcu. Nulla lacinia erat sed est condimentum pellentesque. Sed ante libero, pharetra et ultrices non, porta ac purus.\n' +
                            '\n' +
                            'Cras accumsan libero nec justo ornare mollis. Phasellus cursus dolor non turpis laoreet, non consectetur ante euismod. Proin augue odio, interdum sed ex eget, dapibus feugiat erat. Maecenas id risus neque. Donec ut augue ut ex gravida faucibus. In vitae mi diam. Sed eu tristique enim, a bibendum quam. Phasellus eget mollis tortor. Quisque magna ligula, malesuada non consectetur sed, volutpat quis metus. Mauris et viverra ante. Nam vestibulum risus ut diam lacinia pellentesque. Suspendisse ex sapien, luctus ac massa ac, fermentum imperdiet ante. Praesent euismod ullamcorper iaculis. Vestibulum commodo, odio ac convallis consequat, dolor risus ullamcorper dui, id malesuada mi sapien nec dui.\n' +
                            '\n' +
                            'Nulla placerat leo ut orci volutpat finibus. In eu tristique libero. Sed tincidunt ac nisl non pulvinar. Nullam eget convallis ex. Interdum et malesuada fames ac ante ipsum primis in faucibus. Sed venenatis, eros tristique tristique viverra, ante velit interdum quam, et molestie libero mauris ac eros. Pellentesque aliquet est ligula, vel facilisis dolor elementum at. Donec sed commodo arcu. Duis vitae efficitur erat.\n' +
                            '\n' +
                            'Integer auctor blandit erat in maximus. Mauris rutrum non sapien in fermentum. Pellentesque metus velit, tincidunt sed neque id, pretium gravida nulla. Vestibulum eu sapien nunc. In auctor purus a tortor blandit, eu tempor mauris lobortis. Sed eu leo porttitor, scelerisque tellus eu, pretium turpis. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Proin eget aliquet justo, placerat consectetur ante. Proin blandit tellus sit amet laoreet hendrerit. Praesent a nunc ultrices neque pretium auctor in viverra lacus. Donec quam nunc, facilisis vel sem quis, egestas ullamcorper mi. Praesent rutrum tempor nisi eleifend interdum. Fusce efficitur, ante ac semper blandit, augue augue dictum massa, in elementum leo lectus a lectus. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos.\n' +
                            '\n' +
                            'Phasellus nec elit ac nunc vehicula faucibus. Vestibulum eu venenatis orci. Praesent molestie consectetur tortor, quis volutpat elit malesuada id. Donec vitae felis tellus. Ut laoreet elit condimentum dapibus eleifend. Praesent vel interdum quam. Nunc a est quis urna gravida aliquet a quis risus. Nam feugiat blandit ante, eu pulvinar turpis fringilla pulvinar. Suspendisse potenti. Praesent pretium aliquam ex et volutpat. Proin dictum lacinia risus, at mattis mi vehicula sed. Morbi placerat est sed ante lacinia, non luctus massa rhoncus. Integer sagittis ex facilisis varius iaculis.'
                    }],
                newQuote: {
                    title: '',
                    author: '',
                    from: '',
                    content: ''
                }
            }
        },
        methods: {
            showNotifSuccessAddQuote() {
                const notif = {
                    group: 'general',
                    type: 'success',
                    title: 'Success',
                    text: 'The quote was successfully added'
                };
                this.$emit('show', notif);
            },
            showNotifErrorAddQuote() {
                const notif = {
                    group: 'general',
                    type: 'error',
                    title: 'Error',
                    text: 'The quote hasn\'t been added. Check if all required fields have been filled'
                };
                this.$emit('show', notif);
            },
            addQuote() {
                if (this.newQuote.content !== '') {
                    this.quotes.push({
                        hover: false,
                        title: this.newQuote.title,
                        author: this.newQuote.author,
                        from: this.newQuote.from,
                        content: this.newQuote.content
                    });
                    this.newQuote = {
                        title: '',
                        author: '',
                        from: '',
                        content: ''
                    }
                    this.showNotifSuccessAddQuote();
                }else this.showNotifErrorAddQuote();
            },
            removeQuote(quote) {
                this.quotes = this.quotes.filter(i => i !== quote)
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

    ul {
        margin: 0;
        padding: 0;
        list-style-type: none;
    }

    ul li {
        padding: 10px 30px 50px 30px;
        background-color: #E0EDF4;
        border-left: 5px solid #3EB3F6;
        margin-bottom: 2px;
        color: #3E5252;
        display: inline-block;
        width: 100%;
    }

    .main {
        box-shadow: 0px 20px 40px lightgray;
        margin-bottom: 50px;
    }

    .newQuote {
        width: 100%;
        border: 0;
        padding: 20px;
        font-size: 1.3em;
        background-color: #323333;
        color: #a0adb7;
    }

    textarea {
        resize: vertical;
        overflow: auto;
    }

    input:focus, textarea:focus {
        background-color: #373838;
        outline: none;
    }

    .footer {
        text-align: center;
        padding: 30px 0;
        color: gray;
    }

</style>
