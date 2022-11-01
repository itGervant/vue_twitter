<template>

<input :value="modelValue" @input="updateInput" type="text" class="input">

</template>

<script>

export default {
    name: "my-input",
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateInput(event) {
            this.$emit("update:modelValue", event.target.value)
        }
    }
}
</script>


<style scoped>

.input {
    padding: 10px 15px;
    border: 2px solid blue;
    width: 100%;
    margin-top: 15px;
    margin-bottom: 15px;
}

</style>