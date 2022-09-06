<template>
    <div class="card" @mouseover="deleteAble=true" @mouseout="checkMouseout" :id="cardId">
        <img class="product-img" :src="imgSrc" alt="">
        
        <div v-if="deleteAble" class="delete-product-cont">
            <button class="delete-product" @click="deleteProduct">
                <img class="trashbin" src="trashbin.svg" alt="">
            </button>
        </div>

        <div class="text-block">
            <p class="name">{{ name }}</p>
            <p class="description">{{ description }}</p>
            <p class="price">{{ price }} руб.</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        id:          { type: Number, required: true },
        imgSrc:      { type: String, required: true },
        name:        { type: String, required: true },
        description: { type: String, required: true },
        price:       { type: String, required: true },
    },
    data: () => ({
        deleteAble: false,
    }),
    computed: {
        cardId(){
            return 'card_' + this.id
        }
    },
    methods: {
        deleteProduct() {
            this.$nuxt.$emit('deleteProduct', this.id)
        },
        checkMouseout(event) {
            const outerCont = document.getElementById('cardsContainer');
            const outerCont2 = document.getElementById('header');
            if (event.relatedTarget === outerCont || event.relatedTarget === outerCont2)
                this.deleteAble = false
        }
    }
}
</script>

<style scoped lang="scss">
.card {
    width: 332px;
    height: 423px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    margin-bottom: 16px;
    &:hover {
        cursor: pointer;
    }
}
.product-img {
    width: 332px;
    height: 200px;
    border-radius: 4px 4px 0px 0px;
}
.delete-product-cont {
    display: inline; 
    position: absolute;
    .delete-product {
        position: absolute;
        top: -8px;
        left: -24px;
        width: 32px;
        height: 32px;
        background: #FF8484;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
        border-radius: 10px;
        border-style: none;
        padding: 8px;
        &:hover {
            cursor: pointer;
        }
        .trashbin {
            width: 16px;
            height: 16px;
        }
    }
}
.text-block {
    font-family: 'Source Sans Pro';
    padding: 16px;
    padding-bottom: 24px;

    .name {
        margin: 0px;
        margin-bottom: 16px;
        font-family: inherit;
        font-style: normal;
        font-weight: 600;
        font-size: 20px;
        line-height: 25px;
        color: #3F3F3F;
    }
    .description {
        height: 80px;
        margin: 0px;
        margin-bottom: 32px;
        font-family: inherit;
        font-style: normal;
        font-weight: 400;
        font-size: 16px;
        line-height: 20px;
        color: #3F3F3F;
    }
    .price {
        margin: 0px;
        font-family: inherit;
        font-style: normal;
        font-weight: 600;
        font-size: 24px;
        line-height: 30px;
        color: #3F3F3F;
    }
}
</style>