<template>
    <div class="screen_card">
        <card-flip 
            v-for="(card, index) in cardList" 
            :key="index" 
            :backgroundImg="`images/${card}.png`"
            :card="card"
            :index="index"
            :ref="`card-${index}`"
            @onFlip = "checkRule($event)"
            :cardList="cardList"
        />
    </div>
</template>

<script>
import  CardFlip from './Card.vue'

export default {
    components: {
        CardFlip
    },
    props: {
        cardList: {
            type: Array,
            default: function() {
                return [];
            }
        }
    },
    data() {
        return {
            rules: []
        }
    },
    methods: {
        checkRule(value) {
            if(this.rules.length !==2)
            this.rules.push(value)
            console.log(this.rules)

            //if cardA === cardB => return Right...
            if(this.rules.length === 2 
                && this.rules[0][0] === this.rules[1][0]
                && this.rules[0][1] !== this.rules[1][1]
            ) {
                console.log('Right...')
                //Disable two card
                this.$refs[`card-${this.rules[0][1]}`][0].disableCard()
                this.$refs[`card-${this.rules[1][1]}`][0].disableCard()
                //reset rules to []
                this.rules = []

                const disableElement = document.querySelectorAll('.card.disable')
                if(disableElement && disableElement.length === this.cardList.length - 2) {
                    setTimeout(()=>{
                        this.$emit('onFinish')
                    },650)
                }
            } else 
            if(this.rules.length === 2 
                && (this.rules[0][0] !== this.rules[1][0] 
                || this.rules[0][0] === this.rules[1][0] 
                && this.rules[0][1] === this.rules[1][1])) {
                console.log('Wrong...')
                setTimeout(()=> {
                //Close two card
                this.$refs[`card-${this.rules[0][1]}`][0].closeCard()
                this.$refs[`card-${this.rules[1][1]}`][0].closeCard()
                //reset rules to []
                this.rules = []
                },650)
            } else return false
        }
    }
}
</script>

<style scoped>
    .screen_card {
        width: 720px;
        height: 90vh;
        margin: auto;
        margin-top: 2vh ;
    }

    h1 {
        padding: 2rem 0 ;
        font-size: 46px;
        align-items: center;
    }
</style>
