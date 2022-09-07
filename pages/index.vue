<template>
<div class="root-container">
    <div id="header" class="header">
        <p class="headtitle">Добавление товара</p>
        <div v-if="!isMobile" class="button-container">
            <button id="sortUp" class="button-min" @click="sortList('up')"><img src="sort-up.svg"></button>
            <button id="sortDown" class="button-max" @click="sortList('down')"><img src="sort-down.svg"></button>
            <button id="sortAlpha" class="button-alphabet" @click="sortList('alphabet')"><img src="sort-alphabet.svg"></button>
        </div>
    </div>
    <div class="main">
        <adding-form class="add-form"></adding-form>

        <div v-if="isMobile" class="button-container button-container-mobile">
            <button id="sortUp" class="button-min" @click="sortList('up')"><img src="sort-up.svg"></button>
            <button id="sortDown" class="button-max" @click="sortList('down')"><img src="sort-down.svg"></button>
            <button id="sortAlpha" class="button-alphabet" @click="sortList('alphabet')"><img src="sort-alphabet.svg"></button>
        </div>

        <div class="cards-container" id="cardsContainer">
            <card 
                v-for="(card, i) in cards" :key="i"
                v-bind=card
            ></card>
            <p v-if="emptyList" class="empty-list">Список товаров пуст</p>
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
        cards: cardsList, isMobile: false, emptyList: false,
    }),
    mounted() {
        this.$nuxt.$on('newProduct', this.addProduct);
        this.$nuxt.$on('deleteProduct', this.deleteProduct);

        this.adaptiveSize();
        window.addEventListener('resize', this.adaptiveSize);
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
                this.activateButton('none');
            })
        },
        deleteProduct(id) {
            this.loadAnimation(() => {
                this.cards = this.cards.filter(obj => {
                    return obj.id !== id;
                });
            })
        },
        sortList(how) {
            let callback = () => {};
            if (how=='up') {
                this.activateButton('sortUp')
                callback = () => {
                    this.cards = this.cards.sort((a, b) => 
                        parseFloat(a.price.replace(/\s/g, '')) - parseFloat(b.price.replace(/\s/g, '')));
                }
            }
            else if (how=='down') {
                this.activateButton('sortDown')
                callback = () => {
                    this.cards = this.cards.sort((a, b) => 
                        parseFloat(b.price.replace(/\s/g, '')) - parseFloat(a.price.replace(/\s/g, '')));
                }
            }
            else if (how=='alphabet') {
                this.activateButton('sortAlpha')
                callback = () => {
                    this.cards = this.cards.sort((a, b) => a.name.localeCompare(b.name));
                }
            }
            else return
            this.loadAnimation(callback);
        },
        activateButton(id) {
            document.getElementById('sortUp').removeAttribute('active');
            document.getElementById('sortDown').removeAttribute('active');
            document.getElementById('sortAlpha').removeAttribute('active');
            try {
                document.getElementById(id).setAttribute('active', true);
            } catch(err) { console.log(err) }
        },
        adaptiveSize() {
            const classNames = ['root-container', 'header', 'headtitle', 'main', 'add-form'];
            if (window.innerWidth < 750) {
                this.isMobile = true;
                classNames.forEach(className => {
                    const el = document.getElementsByClassName(className);
                    el.item(0).setAttribute('mobile', true)
                })
            }
            else {
                this.isMobile = false
                classNames.forEach(className => {
                    const el = document.getElementsByClassName(className);
                    el.item(0).removeAttribute('mobile');
                })
            }
        },
    },
    watch: {
        cards: {
            handler() {
                if (this.cards.length == 0)
                    this.emptyList = true
                else
                    this.emptyList = false
            },deep: true
        }
    }
}
</script>

<style scoped lang="scss">

.root-container {
    min-height: 660px;
    padding: 32px;
    padding-right: 16px;
    background: rgba(255, 254, 251, 0.8);

    &[mobile] {
        padding: 0px;
        padding-top: 32px;
    }
}
.header {
    display: flex;
    align-items: flex-start;
    height: 51px;

    .headtitle {
        margin: 0px;
        width: 348px;
        // margin-bottom: 16px;
        font-family: 'Source Sans Pro';
        font-style: normal;
        font-weight: 600;
        font-size: 28px;
        line-height: 35px;

        color: #3F3F3F;

        &[mobile] {
            width: auto;
        }
    }
    &[mobile] {
        justify-content: center;
    }
}
.button-container {
    $bg-color: #b4b4b448;
    $bg-color-active: #b4b4b4c0;
    .button-min {
        width: 65px;
        height: 35px;
        background: $bg-color;
        border-radius: 10px 0px 0px 10px;
        border-style: none;
        &:hover {
            @extend %hover;
        }
    }
    .button-max {
        width: 65px;
        height: 35px;
        background: $bg-color;
        border-radius: 0px;
        border-style: none;
        &:hover {
            @extend %hover;
        }
    }
    .button-alphabet {
        width: 65px;
        height: 35px;
        background: $bg-color;
        border-radius: 0px 10px 10px 0px;
        border-style: none;
        &:hover {
            @extend %hover;
        }
    }
    button[active] {
        background: $bg-color-active;
    }
    img {
        width: 25px;
        height: 25px;
    }
    %hover {
        cursor: pointer;
    }
}
.button-container-mobile {
    margin-top: 35px;
    margin-bottom: 20px;
}

.main {
    display: flex;
    align-items: flex-start;

    &[mobile] {
        flex-direction: column;
        align-items: center;
    }

    .add-form {
        position: sticky;
        top: 24px;

        &[mobile] {
            position: static;
        }
    }
    .cards-container {
        width: 100%;
        min-height: 440px;

        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
        align-items: flex-start;
        align-content: flex-start;

        opacity: 1;
        transition: opacity 0.6s;

        .empty-list {
            margin-top: 200px;
            font-family: inherit;
            font-style: normal;
            font-weight: 600;
            font-size: 30px;
            line-height: 35px;
            text-align: center;
            letter-spacing: -0.02em;
            color: #3f3f3f9a;
        }

        &[load] {
            opacity: 0;
            .card:hover {
                cursor: default;
            }
        }
    }
}
</style>