<template>
    <div class="menubar">
        <ul>
            <li><a href="#">
                <button type="button" class="menu-item active">H</button>
            </a></li>
            <li><a>
                <button type="button" class="menu-item" @click="$emit('addQuote')">+</button>
            </a></li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "Menubar"
    }
</script>

<style scoped>
    .menubar {
        margin-right: 20px;
        padding: 0;
        height: 100%;
        position: fixed;
        top: 0;
        overflow-x: hidden;
        /*overflow-y: scroll;*/
        /*float:left;*/
        background-color: #323333;
    }

    ul {
        margin: 0;
        padding: 0;
        list-style-type: none;
    }

    a {
        text-decoration: none;
    }

    .menu-item {
        width: 48px;
        height: 48px;
        margin: 10px;
        background-color: #464747;
        border-radius: 50px;
        border: transparent 0;
        outline: none;
        font-weight: bold;
        color: white;
        transition-duration: 300ms;
    }

    .active {
        background-color: #3EB3F6;
    }

    .menu-item:hover {
        background-color: #3EB3F6;
        cursor: pointer;
        border-radius: 15px;
        transition-duration: 300ms;
    }

    .menu-item:active {
        transform: translateY(2px);
        transition-duration: 0.5ms;
    }

</style>