<template>
    <button class="tag" type="button" @mouseover="hover = true"
            @mouseleave="hover = false" @click="$emit('removeTag', name)">{{name}} <span v-show="hover === true" class="destroy"> x </span></button>
</template>

<script>
    export default {
        name: 'tag',
        props: ['name'],
        data () {
            return {
                hover: false
            }
        }
    }
</script>

<style>
    .tag {
        border: #E0EDF4 solid;
        border-radius: 20px;
        padding: 2px 10px;
        background-color: transparent;
        color: #a0adb7;
        cursor: pointer;
        margin: 2px 6px;
        outline: none;
    }

    .tag:hover {
        background-color: #4f5151;
    }

    .tag:focus {
        outline: none;
    }

    .destroy {
        color: #E0EDF4;
    }
</style>