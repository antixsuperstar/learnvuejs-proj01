<template>
    <div class="container">
        <div class="row"> <!-- Percentage -->
            <div class="col">
                <h3>Quotes Added</h3>
                <progress :value="quotes.length" max="10"></progress><br/>
                <span>{{ quotes.length }} / 10</span>
            </div>
        </div>
        <div class="row"> <!-- User input -->
            <div class="col-md-8 offset-md-2">
                <div class="row">
                    <div class="col">
                        <h4>Quote</h4>
                    </div>
                </div>
                <div class="row text-center">
                    <div class="col">
                        <textarea
                                class="form-control"
                                v-model="newQuote"
                                id="newquotecontainer"
                                placeholder="Write something inspiring..."></textarea><br />
                        <button
                                class="btn btn-primary"
                                @click="addQuote">Add Quote</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="row mt-4"> <!-- Quote listing -->
            <quote v-for="(q, i) in quotes" :i="i">{{ q }}</quote>
        </div>
    </div>
</template>

<script>
    import { eventbus } from "./main.js";
    import Quote from "./components/Quote.vue";

    export default {
        data: function() {
            return {
                quotes: [
                    'This is a quote',
                    'This is another quote',
                    'This is a much much longer quote'
                ],
                newQuote: ''
            }
        },
        components: {
            Quote
        },
        methods: {
            addQuote: function() {
                // Let's do some basic validation
                switch (true) {
                    case !this.newQuote.length: // There is no text to add
                        alert('Add some text before clicking the button :)');
                        break;
                    case this.quotes.length==10: // Reached maximum!
                        alert('I can only add up to ten quotes :(');
                        break;
                    default: // Nothing unusual, let's add that wonderful quote!
                        this.quotes.push(this.newQuote);
                        this.newQuote = '';
                        break;
                }
                document.getElementById('newquotecontainer').focus();
            }
        },
        created() {
            eventbus.$on('removeQuote', event => {
                let id = event.target.getAttribute('qid');
                this.quotes.splice(id, 1);
            });
        }
    }

</script>

<style scoped>
    progress {
        width: 100%;
        height: 2em;
        margin: auto;
        border: 1px;
        border-radius: 5px;
        content:'fdsa'
    }
</style>
