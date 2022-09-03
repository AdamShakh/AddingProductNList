<template>
    <div class="adding-form">

        <p>Наименование товара</p>
        <input type="text" placeholder="Введите наименование товара">

        <p>Описание товара</p>
        <input type="text" placeholder="Введите описание товара" style="height: 108px;">

        <p>Ссылка на изображение товара</p>
        <input type="text" placeholder="Введите ссылку">

        <p>Цена товара</p>
        <input type="text" placeholder="Введите цену">

        <button>Добавить товар</button>

    </div>
</template>

<style scoped>
.adding-form {
    width: 332px;
    height: 440px;
    padding: 24px;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
}
p {
    margin-bottom: 4px;
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: #49485E;
}
input {
    width: 284px;
    height: 36px;
    margin-bottom: 16px;
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    border-style: none;
    
    
}
input::-webkit-input-placeholder {
    color: #B4B4B4; 
    margin-left: 16px;
    margin-top: 10px;
    position: fixed;
}
input::-moz-placeholder {
    color: #B4B4B4; 
    margin-left: 16px;
    margin-top: 10px;
    position: fixed;
}
input:-moz-placeholder {
    color: #B4B4B4; 
    margin-left: 16px;
    margin-top: 10px;
    position: fixed;
}
input:-ms-input-placeholder {
    color: #B4B4B4; 
    margin-left: 16px;
    margin-top: 10px;
    position: fixed;
}

button {
    width: 284px;
    height: 36px;
    margin-top: 8px;
    background: #EEEEEE;
    border-radius: 10px;
    border-style: none;
}
</style>