<template>
<button class="btn">
<slot></slot>
</button>


</template>

<script>
export default {
    name: "my-button",
}

</script>

<style scoped>

.btn {
    background: none;
    align-self: flex-end;
    width: 150px;
    height: 50px;
    color: teal;
}

</style>