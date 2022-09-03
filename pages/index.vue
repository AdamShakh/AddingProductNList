<template>
<div class="rootContainer">
    <span class="headline">Добавление товара</span>
    <div class="container">
        <adding-form></adding-form>

        <div class="cardsContainer">
            <!-- <card 
                v-for="(card, i) in cardsList" :key="i"
                v-bind=card
            ></card> -->
        </div>
    </div>
</div>
</template>

<script>
import AddingForm from '@/components/AddingForm.vue'
// import Card from '@/components/Card.vue'
// import cardsModel from '@/store/cards.json'

export default {
    name: 'IndexPage',
    components: {
        AddingForm, 
        // Card
    },
    created() {
        // this.cardsList = cardsModel
    },
    beforeDestroy(){

    }
}
</script>

<style scoped>
.rootContainer {
    /* background: #E5E5E5; */
}
.container {
    display: flex;
    align-items: flex-start;
}

.cardsContainer {
    flex-direction: row;
    flex-wrap: wrap;

}
.headline {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;

    color: #3F3F3F;
}

</style>