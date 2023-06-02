<template>
    <div class="screen">
        <h1>POKE MEMORIES</h1>
        <h3>Select mode to start game</h3>
        <div class="action">
            <button @click="onStart(16)"> 
                <span>4x4</span>
                <span>Easy</span>
            </button>

            <button @click="onStart(36)"> 
                <span>6x6</span>
                <span>Normal</span>
            </button>

            <button @click="onStart(64)"> 
                <span>8x8</span>
                <span>Hard</span>
            </button>

            <button @click="onStart(100)"> 
                <span>10x10</span>
                <span>Super Hard</span>
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                
            }
        },
        methods: {
            onStart (totalBlock) {
                this.$emit("onPlay", { "totalBlock": totalBlock })
            }
        },
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

    h3 {
        font-size: 28px;
    }

    .action {
        display: flex;
        margin-top: 1.5rem ;
    }

    button {
        font: var(--font);  
        width: 120px;
        height: 120px;
        background: #000000;
        box-shadow: none;
        border: 1px solid var(--light);
        color: var(--light);
        display: flex;
        flex-direction: column;
        border-radius: 1rem;
        margin: 0 1rem;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        transition: background 0.3s ease-in-out;
    }

    button:hover {
        opacity: 0.9;
        scale: 1.04;
    }

</style>