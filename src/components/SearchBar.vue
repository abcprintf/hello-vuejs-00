<template>
    <div>
        <input v-on:input="onInput" />
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
    methods: {
        onInput: function(event) {
            if(event.target.value.length > 3){
                this.$emit('termChange', event.target.value);
            }else{
                this.$emit('termChange', null);
            }
        }
    }
}
</script>

<style scoped>
    input {
        width: 75%;
    }

    div {
        text-align: center;
        margin: 20px;
    }
</style>