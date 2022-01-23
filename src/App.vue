<template>
    <div id="app">
        <AddCard
            @resivedData="pushData"
            @changeView="showAddCard = !showAddCard"
            v-if="showAddCard"
            :cards="array"
        />
        <Home
            @removeCard="removeCard"
            :cards="array"
            @changeView="showAddCard = !showAddCard"
            v-else
        />
    </div>
</template>

<script>
import AddCard from "./view/AddCard.vue";
import Home from "./view/Home.vue";

export default {
    name: "App",
    data() {
        return {
            showAddCard: false,
            array: [
                {
                    cardNumber: "2347567645654565",
                    cardholder: "Daniel Amalraj",
                    expireMonth: "2022/21",
                    CCV: "987",
                    vendor: "Bitcoin Inc",
                },
                {
                    cardNumber: "8657567645654565",
                    cardholder: "Matthew Amalraj",
                    expireMonth: "2022/21",
                    CCV: "987",
                    vendor: "Blockchain Inc",
                },
                {
                    cardNumber: "8767864645654565",
                    cardholder: "Luka Amalraj",
                    expireMonth: "2022/21",
                    CCV: "987",
                    vendor: "Ninja Bank",
                },
            ],
        };
    },
    created() {
        let savedData = JSON.parse(localStorage.getItem("cards"));

        if (savedData) {
            this.array = savedData;
        }
    },
    components: {
        Home,
        AddCard,
    },
    methods: {
        pushData(data) {
            this.array.push(data);
            localStorage.setItem("cards", JSON.stringify(this.array));
        },
        removeCard(array) {
            this.array = this.array.filter((card) => {
                return card.cardNumber != array.cardNumber;
            });
            localStorage.setItem("cards", JSON.stringify(this.array));
        },
    },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=PT+Mono&family=Source+Sans+Pro:wght@700&display=swap");
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    display: flex;
    // justify-content: center;

    h1 {
        font-family: "Source Sans Pro", sans-serif;
        text-transform: uppercase;
        font-size: 32px;
    }
    p {
        font-family: "PT Mono", monospace;
        text-transform: uppercase;
        font-size: 14px;
    }

    button {
        font-family: "PT Mono", monospace;
        text-transform: uppercase;
        padding: 1rem;
        border-radius: 8px;
        font-weight: bold;
        font-size: 16px;
    }
    button:hover {
        background-color: black;
        color: white;
    }
}
</style>
