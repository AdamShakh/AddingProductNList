<template>
    <div id="adding-form">

        <p required>Наименование товара</p>
        <input type="text" placeholder="Введите наименование товара">

        <p>Описание товара</p>
        <textarea placeholder="Введите описание товара" style="height: 97px; padding-top: 11px;"></textarea>

        <p required>Ссылка на изображение товара</p>
        <input type="text" placeholder="Введите ссылку">

        <p required>Цена товара</p>
        <input type="text" placeholder="Введите цену">

        <button>Добавить товар</button>

    </div>
</template>

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
    margin-bottom: 16px;
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
input::placeholder, textarea::placeholder {
    color: #B4B4B4;
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