<template>
    <input class="input" type="text" ref="input" :value="value"
        @input="input" @focus="$emit('focus')" @blur="$emit('blur')"
        @keydown.down.exact.prevent="$emit('complete-next')"
        @keydown.up.exact.prevent="$emit('complete-prev')"
        @keydown.down.ctrl.exact.prevent="$emit('eng-next')"
        @keydown.up.ctrl.exact.prevent="$emit('eng-prev')"
        autocomplete="off" autofocus="autofocus" spellcheck="false"
        placeholder="👴 搜点什么？">
</template>

<script>
export default {
    model: {
        prop: 'value',
        event: 'input',
    },
    props: {
        value: {
            type: String,
            default: function() {
                return '';
            }
        },
        event: {
            required: true,
        }
    },
    methods: {
        input: function(event) {
            this.$emit('input', event.target.value)
        },
        focus: function() {
            this.$refs.input.focus();
        },
    },
    created: function() {
        this.event.$on('focus', this.focus);
    }
}
</script>

<style scoped>
.input {
    width: 0;
    padding: var(--v-spacing) var(--h-spacing);
    border: none;
    font-size: 1rem;
    line-height: 1.5rem;
    flex-grow: 1;
    background: transparent;
}
</style>