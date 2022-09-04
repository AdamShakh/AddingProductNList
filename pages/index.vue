<template>
<div class="rootContainer">
    <p class="headtitle">Добавление товара</p>
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
    padding: 32px;
    background: rgba(255, 254, 251, 0.8);
}
.container {
    display: flex;
    align-items: flex-start;
}
.cardsContainer {
    flex-direction: row;
    flex-wrap: wrap;

}
.headtitle {
    margin: 0px;
    margin-bottom: 16px;
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;

    color: #3F3F3F;
}
</style>