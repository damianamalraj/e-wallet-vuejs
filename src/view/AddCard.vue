<template>
    <div class="add-card">
        <h1>
            Add a new <br />
            banK card
        </h1>
        <Card :array="array" />
        <br />
        <form @submit.prevent="sendData">
            <div>
                <p>card number</p>
                <input v-model="array.cardNumber" type="text" /><br />
            </div>
            <div>
                <p>cardholder name</p>
                <input v-model="array.cardholder" type="text" /><br />
            </div>
            <section>
                <div>
                    <p>valid thru</p>
                    <input v-model="array.expireMonth" type="month" /><br />
                </div>
                <div>
                    <p>ccv</p>
                    <input v-model="array.CCV" type="text" />
                </div>
            </section>
            <div>
                <p>vendor</p>
                <select v-model="array.vendor" type="options">
                    <option></option>
                    <option value="Bitcoin Inc">Bitcoin Inc</option>
                    <option value="Blockchain Inc">Blockchain Inc</option>
                    <option value="Evil Corp">Evil Corp</option>
                    <option value="Ninja Bank">Ninja Bank</option>
                </select>
                <br />
            </div>
            <button>Submit</button>
        </form>
        <button @click="$emit('changeView')">add card</button>
    </div>
</template>

<script>
import Card from "../components/Card.vue";
export default {
    data() {
        return {
            array: {
                cardNumber: "",
                cardholder: "",
                expireMonth: "",
                CCV: "",
                vendor: "",
            },
        };
    },
    methods: {
        sendData() {
            this.$emit("resivedData", "data");
            console.log(this.array);
        },
    },
    components: {
        Card,
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.add-card {
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 414px;
    height: 896px;
    background-color: whitesmoke;

    form {
        display: flex;
        flex-direction: column;

        div {
            display: flex;
            flex-direction: column;
            p {
                align-self: flex-start;
                margin: 0;
            }
            input,
            select {
                height: 2rem;
            }
        }
        section {
            display: flex;
            justify-content: space-between;

            input {
                width: 190px;
            }
        }
    }
}
</style>
