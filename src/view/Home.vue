<template>
    <div class="home">
        <h1>e-wallet</h1>
        <p>active card</p>
        <Card />
        <br />
        <div class="cards-list">
            <Card
                class="list-item"
                :array="array"
                v-for="array in cards"
                :key="array"
            />
        </div>
        <br />
        <button @click="$emit('changeView')">Add a new card</button>
    </div>
</template>

<script>
import Card from "../components/Card.vue";
export default {
    data() {
        return {};
    },
    props: ["cards"],
    components: { Card },
};
</script>

<style scoped lang="scss">
.home {
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 400px;
    height: 750px;
    background-color: whitesmoke;
}

.cards-list {
    display: flex;
    flex-direction: column;
    max-height: 400px;
}
.list-item:nth-of-type(2) {
    transform: translateY(-80%);
}
.list-item:nth-of-type(3) {
    transform: translateY(-160%);
}
.list-item:nth-of-type(4) {
    transform: translateY(-240%);
}
.list-item:nth-of-type(5) {
    transform: translateY(-320%);
}
.list-item:nth-of-type(6) {
    transform: translateY(-400%);
}
.list-item:nth-of-type(7) {
    transform: translateY(-480%);
}
</style>
