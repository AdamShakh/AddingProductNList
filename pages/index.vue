<template>
<div class="root-container">
    <div id="header" class="header">
        <p class="headtitle">Добавление товара</p>
    </div>
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
import cardsList from '@/static/products.json'

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
        this.$nuxt.$on('deleteProduct', this.deleteProduct);
    },
    methods: {
        loadAnimation(callback) {
            let container = document.getElementById('cardsContainer');
            container.setAttribute('load', true);
            setTimeout(() => {
                callback();
                container.removeAttribute('load');
            }, 1000);
        },
        addProduct(product) {
            this.loadAnimation(() => {
                product.id = 1;
                this.cards.forEach(obj => {
                    if (obj.id > product.id) product.id = obj.id + 1;
                })
                this.cards.unshift(product);
            })
        },
        deleteProduct(id) {
            this.loadAnimation(() => {
                this.cards = this.cards.filter(obj => {
                    return obj.id !== id;
                });
            })
        }
    },
        }
    }
}
</script>

<style scoped lang="scss">
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
.header {
    height: 51px;
}
.headtitle {
    margin: 0px;
    // margin-bottom: 16px;
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;

    color: #3F3F3F;
}
</style>