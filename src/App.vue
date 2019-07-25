<template>
    <div id="app">
        <Menubar @addQuote="addingQuote = !addingQuote"></Menubar>
        <notifications group="general"
                       position="top right"
                       :speed="700" :duration="6000" :width="400" class="notification-title notification-content"/>
        <h1>Kipmi</h1>
        <div class="main">
            <!--<AddQuote :tags="tags" @addQuote="addQuote" @addTag="addTag"
                      @showNotifSuccessAddQuote="showNotifSuccessAddQuote"
                      @showNotifErrorAddQuote="showNotifErrorAddQuote"></AddQuote>-->
            <input type="text" placeholder="Search...">
            <AddQuote @addQuote="addQuote" @showNotifSuccessAddTag="showNotifSuccessAddTag" @showNotifErrorAddQuote="showNotifErrorAddQuote" :tags="tags" v-if="addingQuote === true"></AddQuote>
            <Quotes :quotes="quotes" :tags="tags" @removeQuote="removeQuote" @show="show"></Quotes>
            <footer class="footer">
                <p> Keep in mind.</p>
            </footer>
        </div>
    </div>
</template>

<script>
    import Quotes from './components/Quotes.vue'
    import AddQuote from './components/AddQuote.vue'
    import Menubar from "./components/Menubar";

    export default {
        name: 'app',
        components: {
            Menubar,
            Quotes,
            AddQuote
        },
        data() {
            return {
                addingQuote: false,
                quotes: [
                    {
                        hover: false,
                        title: 'quote 1',
                        author: '',
                        from: 'Somewhere',
                        content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed at rhoncus est. Fusce felis sem, dignissim vel felis sit amet, scelerisque tempus orci. Quisque malesuada neque a leo viverra, a pharetra dui maximus. Curabitur nunc purus, porta et nisi ultricies, feugiat gravida velit. Donec ac semper arcu. Nulla lacinia erat sed est condimentum pellentesque. Sed ante libero, pharetra et ultrices non.',
                        tags: ['earth']
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
                            'Phasellus nec elit ac nunc vehicula faucibus. Vestibulum eu venenatis orci. Praesent molestie consectetur tortor, quis volutpat elit malesuada id. Donec vitae felis tellus. Ut laoreet elit condimentum dapibus eleifend. Praesent vel interdum quam. Nunc a est quis urna gravida aliquet a quis risus. Nam feugiat blandit ante, eu pulvinar turpis fringilla pulvinar. Suspendisse potenti. Praesent pretium aliquam ex et volutpat. Proin dictum lacinia risus, at mattis mi vehicula sed. Morbi placerat est sed ante lacinia, non luctus massa rhoncus. Integer sagittis ex facilisis varius iaculis.',
                        tags: ['life', 'people']
                    }],
                tags: ['life', 'work', 'earth', 'people']
            }
        },
        methods: {
            show(notif) {
                this.$notify(notif)
            },
            clean(group) {
                this.$notify({group, clean: true})
            },
            showNotifSuccessAddQuote(item) {
                const notif = {
                    group: 'general',
                    type: 'success',
                    title: 'Success',
                    text: 'The quote ' + item + '  was successfully added'
                };
                this.show(notif);
            },
            showNotifErrorAddQuote() {
                const notif = {
                    group: 'general',
                    type: 'error',
                    title: 'Error',
                    text: 'The quote hasn\'t been added. Check if all required fields have been filled'
                };
                this.show(notif);
            },
            showNotifSuccessAddTag(item) {
                const notif = {
                    group: 'general',
                    type: 'success',
                    title: 'Success',
                    text: 'The tag #' + item + ' was successfully created'
                };
                this.show(notif);
            },
            addQuote(newQuote) {
                this.quotes.push(newQuote);
                this.showNotifSuccessAddQuote(newQuote.title);
            },
            removeQuote(quote) {
                this.quotes = this.quotes.filter(i => i !== quote)
            },
            addTag(tag) {
                this.tags.push(tag);
            }
        }
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Montserrat:400,700');
    @import "https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css";
    @import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
    @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

    body, html {
        margin: 0;
        height: 100%;
    }

    body {
        background-color: #EEEEEE;
        font-family: 'Montserrat', sans-serif;
        font-size: 1.3em;
        justify-items: center;
        align-items: center;
    }

    h1 {
        text-align: center;
        font-size: 4em;
        margin: 30px;
    }

    a {
        color: #3EB3F6;
    }

    a:hover {
        color: #3E5252;
        text-decoration: underline;
    }

    input, textarea {
        width: 100%;
        border: 0;
        padding: 20px;
        font-size: 1em;
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

    .main {
        width: 80%;
        margin-right: auto;
        margin-left: auto;
        box-shadow: 0px 20px 40px lightgray;
        margin-bottom: 50px;
    }

    .footer {
        text-align: center;
        padding: 30px 0;
        color: gray;
    }

    .notification-title {
        font-size: 2em;
    }

    .notification-content {
        font-size: 1.5em;
    }
</style>
