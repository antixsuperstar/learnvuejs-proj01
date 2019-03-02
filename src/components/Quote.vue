<template>
    <div class="col-6 col-md-2 quote">
        <p
                @click="removeQuote"
                :qid="i"
                class="text-center">
            <slot></slot>
        </p>
    </div>
</template>

<script>
    import { eventbus } from "../main";

    export default {
        props: [
            'i'
        ],
        methods: {
            removeQuote: function(event) {
                eventbus.$emit('removeQuote', event);
            }
        }
    }
</script>

<style scoped>
    div.quote > p {
        cursor: pointer;
        font-family: 'Comic Sans MS', sans-serif;
        border: thin solid lightgray;
        border-radius: 0.5rem;
        padding: 1rem;
    }
</style>