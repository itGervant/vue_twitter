<template>
<div class="window" v-if="show === true" @click="hideWindow">
    <div @click.stop class="window__content">
        <slot></slot>
    </div>
</div>

</template>

<script>
export default {
    name: 'my-window',
    props: {
        show: {
            type: Boolean,
            default: false,
        }
    },
    methods: {
        hideWindow() {
            this.$emit('update:show', false)
        }
    }
}

</script>


<style>
.window {
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display: flex;
}

.window__content {
    margin: auto;
    background: white;
    border-radius: 15px;
    min-height: 50px;
    min-width: 300px;
    padding: 20px;
    border: 2px solid green;
}

</style>