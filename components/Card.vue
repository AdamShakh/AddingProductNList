<template>
    <div class="card">
        <img :src="imgSrc" alt="Продукт">
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
        imgSrc:      { type: String, required: true },
        name:        { type: String, required: true },
        description: { type: String, required: true },
        price:       { type: String, required: true },
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
img {
    width: 332px;
    height: 200px;
    border-radius: 4px 4px 0px 0px;
}
.text-block {
    font-family: 'Source Sans Pro';
    padding: 16px;
    padding-bottom: 24px;
}
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
</style>