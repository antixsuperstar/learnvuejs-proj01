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
                        <textarea class="form-control"></textarea><br />
                        <button class="btn btn-primary">Add Quote</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="row mt-4"> <!-- Quote listing -->
            <div
                    v-for="(q, i) in quotes"
                    class="col-6 col-md-2 quote">
                <p
                        @click="removeQuote"
                        :qid="i"
                        class="text-center">{{ q }}</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                quotes: [
                    'This is a quote',
                    'This is another quote',
                    'This is a much much longer quote'
                ]
            }
        },
        methods: {
            removeQuote: function(event) {
                console.log(event.target.$attrs('qid'));
            }
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
    div.quote > p {
        cursor: pointer;
        font-family: 'Comic Sans MS';
        border: thin solid lightgray;
        border-radius: 0.5rem;
        padding: 1rem;
    }
</style>
