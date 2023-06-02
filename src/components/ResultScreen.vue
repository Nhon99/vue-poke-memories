<template>
    <div class="screen">
        <h1 class="header">✨ Congratulations ✨</h1>
        <p class="time">{{ timePlay }} seconds</p>
        <button @click="onStartAgain">Start Again</button>
    </div>
</template>

<script>
export default {
    data() {

    },
    methods: {
        onStartAgain() {
            this.$emit('onStartAgain')
        }
    },
    props: {
        timePlay: {
            tyle: Number,
            default: 0
        }
    }
}
</script>


<style scoped>
    .screen {
        width: 100vw;
        height: 92vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: rgb(160, 252, 221);
    }

    h1 {
        font-size: 46px
    }

    p {
        font-size: 28px;
    }

    button {
        width: 120px;
        height: 50px;
        display: inline-block;
        margin-top: 1rem;
        background-color: black;
        color: #fff;
        border: none;
        border-radius: 8px ;
        font-size: 16px;
    }

    button:hover {
        cursor: pointer;
        opacity: 0.8;
    }
</style>