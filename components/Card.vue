<template>
    <div class="card">
        <img :src="imgSrc" alt="">
        <div class="text-block">
            <h3 class="name">{{ name }}</h3>
            <p class="description">{{ description }}</p>
            <span class="price">{{ price }} руб.</span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'card',
    props: {
        imgSrc:      { type: String, required: true },
        name:        { type: String, required: true },
        description: { type: String, required: true },
        price:       { type: String, required: true },
    },
}
</script>

<style scoped>

.card {
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
}
img {
    width: 332px;
    height: 200px;
    border-radius: 4px 4px 0px 0px;
}
.text-block {
    padding: 16px;
    padding-top: 16px;
    padding-bottom: 24px;
}
.name {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;
    color: #3F3F3F;
}
.description {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 20px;
    color: #3F3F3F;
}
.price {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
    color: #3F3F3F;
}

</style>