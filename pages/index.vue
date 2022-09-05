<template>
<div class="root-container">
    <p class="headtitle">Добавление товара</p>
    <div class="container">
        <adding-form></adding-form>

        <div class="cards-container" id="cardsContainer">
            <card 
                v-for="(card, i) in cards" :key="i"
                v-bind=card
            ></card>
        </div>
    </div>
</div>
</template>

<script>
import AddingForm from '@/components/AddingForm.vue'
import Card from '@/components/Card.vue'
import cardsList from '@/static/cards.json'

export default {
    name: 'IndexPage',
    components: {
        AddingForm, Card,
    },
    data: () => ({
        cards: cardsList,
    }),
    created() {
        this.$nuxt.$on('newProduct', this.addProduct);
    },
    methods: {
        addProduct(product) {
            let container = document.getElementById('cardsContainer');
            container.setAttribute('load', true);
            setTimeout(() => {
                product.id = this.cards.length;
                this.cards.unshift(product);

                container.removeAttribute('load');
            }, 1000);
        }
    }
}
</script>

<style scoped>
.root-container {
    padding: 32px;
    padding-right: 24px;/**/
    background: rgba(255, 254, 251, 0.8);
}
.container {
    display: flex;
    align-items: flex-start;
}
.cards-container {
    margin-left: 8px;/*16px;*/

    display: flex;
    flex-wrap: wrap;
    justify-content: space-around; /*space-evenly;*/
    align-content: flex-start;
    align-items: flex-start;

    opacity: 1;
    transition: opacity 0.6s;
}
.cards-container[load] {
    opacity: 0;
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