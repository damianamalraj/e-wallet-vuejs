<template>
    <div class="home">
        <h1>e-wallet</h1>
        <p>active card</p>
        <Card :array="current" />
        <br />
        <div class="cards-list">
            <a
                class="list-item"
                @click="change(array)"
                v-for="array in cards"
                :key="array.cardNumber"
            >
                <Card :array="array" />
            </a>
        </div>
        <br />
        <button @click="$emit('changeView')">Add a new card</button>
    </div>
</template>

<script>
import Card from "../components/Card.vue";
export default {
    data() {
        return {
            current: this.cards[0],
            show: false,
        };
    },
    props: ["cards"],
    components: { Card },
    methods: {
        change(x) {
            this.current = x;
        },
    },
};
</script>

<style scoped lang="scss">
.home {
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 414px;
    height: 896px;
    background-color: whitesmoke;
}

.cards-list {
    display: flex;
    flex-direction: column;
    max-height: 400px;
}

.list-item {
    cursor: pointer;
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
