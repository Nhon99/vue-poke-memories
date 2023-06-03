<template>
    <div 
        class="card" 
        :class="{'disable': disable}"
        :style="{
            width: `${(620 - 5*2*Math.sqrt(cardList.length))/Math.sqrt(cardList.length)}px`,
            height: `${(620 - 5*2*Math.sqrt(cardList.length))/Math.sqrt(cardList.length)}px`
        }"
    >
        <div class="card__inner" :class="{'is-flipped': isChoose }" @click="chooseCard" >
            <div class="card__face card__face--font">
                <div class="card__content"></div>
            </div>

            <div class="card__face card__face--back">
                <div class="card__content" :style="{backgroundImage: `url('@/assets/${backgroundImg}')`}">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                isChoose:false,
                disable: false,
            }
        },
        props: {
            backgroundImg: {
                tyle: String,
            },
            card: {
                tyle: [String, Number, Array, Object]
            },
            index: {
                tyle: Number,
            },
            cardList: {
                tyle: Array,
                default: []
            }
        },
        methods: {
            chooseCard () {
                if(this.disable) return false
                this.isChoose= !this.isChoose
                console.log(this.isChoose)
                if(this.isChoose) this.$emit('onFlip',[this.card, this.index])
            },
            closeCard () {
                this.isChoose = false
            },
            disableCard () {
                this.disable = true
            }
        },
    }
</script>

<style scoped>
    .card {
        display: inline-block;
        margin: 0.4rem;
        width: 92px;
        height: 92px;
        border-radius: 50px;
    }

    .card.disable .card__inner {
        cursor: default;
    }

    .card__inner {
        width: 100%;
        height: 100%;
        transition: transform 1s;
        transform-style: preserve-3d;
        cursor: pointer;
        position: relative;
        
    }

    .card__inner.is-flipped {
        transform: rotateY(-180deg);
    }

    .card__face {
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        backface-visibility: hidden;
        width: 100%;
        height: 100%;
        border-radius: 1rem;
        box-shadow: 2px 2px 10px 1px #827c7c;
    }

    .card__face--back {
        transform: rotateY(-180deg);
    }

    .card__face--back .card__content {
        width: 100%;
        height: 100%;
        background-position: center;
        background-repeat: no-repeat;
        background-size: 80%;
    }

    .card__face--font .card__content {
        background-image: url('../assets/images/icon_back.png');
        background-position: center center;
        background-size: 60%;
        background-repeat: no-repeat ;
        width: 100%;
        height: 100%;
    }

</style>
