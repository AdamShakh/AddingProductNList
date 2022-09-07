<template>
    <div id="adding-form">

        <div class="field">
            <p required>Наименование товара</p>
            <input id="name" v-model="name" type="text" placeholder="Введите наименование товара">
        </div>

        <div class="field">
            <p>Описание товара</p>
            <textarea id="desc" v-model="desc" maxlength="185" placeholder="Введите описание товара">
            </textarea>
        </div>

        <div class="field">
            <p required>Ссылка на изображение товара</p>
            <input id="src" v-model="src" type="text" placeholder="Введите ссылку">
        </div>

        <div class="field">
            <p required>Цена товара</p>
            <input id="price" v-model="price" type="text" placeholder="Введите цену">
        </div>

        <button id="addBtn" :class="{ 'button-active' : activeSubmit }" 
                @click="submit" :disabled="!activeSubmit"
                >Добавить товар
        </button>

    </div>
</template>

<script>
export default {
    name: 'AddingForm',
    data: () => ({
        name: '', desc: '', src: '', price: '',
        isValid: {name: false, src: false, price: false}, activeSubmit: false,
    }),
    mounted() {
        this.addInvalidityCheck('name');
        this.addInvalidityCheck('src');
        this.addInvalidityCheck('price');
    },
    methods: {
        addInvalidityCheck(id) {
            const el = document.getElementById(id);
            el.addEventListener('input', (event) => {
                if (!el.value) {
                    event.target.setAttribute('invalid', true)
                    event.target.parentNode.setAttribute('warning', true)
                    this.isValid[id] = false;
                } else {
                    event.target.removeAttribute('invalid')
                    event.target.parentNode.removeAttribute('warning')
                    this.isValid[id] = true;
                }
            });
        },
        submit() {
            let product = {
                imgSrc:   this.src, 
                name:  this.name, 
                description:  this.desc,
                price: this.price,
            }
            this.$nuxt.$emit('newProduct', product);
            this.reset();
            this.successfulSubmit();
        },
        reset() {
            this.name = this.desc = this.src = this.price = '';
            this.isValid = {name: false, src: false, price: false};
            this.activeSubmit = false;
        },
        successfulSubmit() {
            const fields = ['name', 'desc', 'src', 'price'];
            let names = [];
            fields.forEach(field => {
                names.push(document.getElementById(field))
            });
            names.forEach(field => {
                field.setAttribute('success', true);
            })
            setTimeout(() => {
                names.forEach(field => {
                    field.removeAttribute('success');
                })
            }, 1000);
        },
        kMask (num) {
            while (num.indexOf(' ') !== -1)
                num = num.replace(' ', '')
            let n = num.toString();
            return n.replace(/(\d{1,3}(?=(?:\d\d\d)+(?!\d)))/g, "$1" + " ");
        }
    },
    watch: {
        isValid: {
            handler (isIt) {
                if (isIt.name == true && isIt.src == true && isIt.price == true)
                    this.activeSubmit = true;
                else 
                    this.activeSubmit = false;
            },deep: true
        },
        price(price) {
            if (!/^\d+$/.test(price.slice(-1))) {
                this.price = price.replace(price.slice(-1), '')
            }
            else {
                this.price = this.kMask(price)
            }
        },
    },
}
</script>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css?family=Inter');

#adding-form {
    font-family: 'Source Sans Pro';
    font-weight: 400;
    width: 284px;
    padding: 24px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
}
.field {
    margin-bottom: 16px;
}
p {
    margin: 0px;
    margin-bottom: 4px;
    font-family: inherit;
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #49485E;
}
p[required]::after {
    content: '';
    position: absolute;
    width: 4px;
    height: 4px;
    background: #FF8484;
    border-radius: 4px;
}
input[type="text"], textarea {
    min-width: 252px;
    max-width: 252px;
    height: 36px;
    margin: 0;
    padding: 0px;
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border-style: none;
    
    font-family: inherit;
    font-style: normal;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    color: #3F3F3F;
    padding-left: 16px;
    padding-right: 16px;
    resize: none;
    vertical-align: top;
}
textarea {
    height: 97px;
    padding-top: 11px;
}
input::placeholder, textarea::placeholder {
    color: #B4B4B4;
    transition: color 1s;
}
input::placeholder {
    margin-top: 11px;
}
input:focus, textarea:focus {
    outline: 0;
    color: #212529;
    background-color: #fff;
    border-color: #bdbdbd;
    box-shadow: 0 0 0 0.2rem rgba(158, 158, 158, 0.25);
}
input[invalid] {
    border: 1px solid #FF8484;
    box-sizing: border-box;
    min-width: 284px;
}
div[warning]::after {
    display: block;
    content: 'Поле является обязательным';
    position: absolute;
    margin-top: 4px;
    font-family: inherit;
    font-style: normal;
    font-weight: 400;
    font-size: 8px;
    line-height: 10px;
    letter-spacing: -0.02em;
    color: #FF8484;
}
input[success] {
    border: 1px solid #88ff84;
    box-sizing: border-box;
    min-width: 284px;
}
textarea[success] {
    height: 108px;
    padding-top: 11px;
    border: 1px solid #88ff84;
    box-sizing: border-box;
    min-width: 284px;
}
input[success]::placeholder, textarea[success]::placeholder {
    color: #FFFEFB;
}

button {
    width: 284px;
    height: 36px;
    margin-top: 8px;
    background: #EEEEEE;
    border-radius: 10px;
    border-style: none;

    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 15px;
    text-align: center;
    letter-spacing: -0.02em;
    color: #B4B4B4;
}
.button-active {
    background: #7BAE73; 
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1); 
    border-radius: 10px;
    font-weight: 400;//
    letter-spacing: 0em;
    color: #FFFFFF; 
    &:hover {
        color: rgb(223, 253, 90);
        cursor: pointer;
    }
}

input::-webkit-input-placeholder {
    color: #B4B4B4;
    margin-top: 11px;
}
input::-moz-placeholder {
    color: #B4B4B4;
    margin-top: 11px;
}
input:-moz-placeholder {
    color: #B4B4B4;
    margin-top: 11px;
}
input:-ms-input-placeholder {
    color: #B4B4B4;
    margin-top: 11px;
}
</style>