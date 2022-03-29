<template>
    <button @click="handleClick">
        <slot></slot>
    </button>
</template>

<style scoped>
    button {
        appearance: none;
        -webkit-appearance: none;
        border: none;
        background-color: #2e3d50;
        color: #f9f9f9;
        border-radius: 25px;
        padding: 10px 15px;
        cursor: pointer;
        box-shadow: 0 10px 20px rgba(0,0,0,.1);
        transition: box-shadow .2s ease-in-out;
        font-weight: bold;
        text-transform: uppercase;
        font-size: 9px;
        letter-spacing: -.01em;
    }

    button:hover {
        box-shadow: 0 0 5px rgba(0,0,0,.1);
    }
</style>

<script>
export default {
    name: 'Button',
    methods: {
        handleClick() {
            this.$emit('handleClick')
        }
    }
}
</script>