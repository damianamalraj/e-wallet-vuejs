<template>
    <div class="add-card">
        <a @click="$emit('changeView')" class="Back">Back</a>
        <h1>
            Add a new <br />
            banK card
        </h1>
        <Card :card="array" />
        <br />
        <form @submit.prevent="">
            <div>
                <p>card number</p>
                <input
                    :class="[
                        { error: showNumberError },
                        { error: showDuplicateError },
                    ]"
                    v-model="array.cardNumber"
                    type="text"
                    maxlength="16"
                /><br />
            </div>
            <div>
                <p>cardholder name</p>
                <input
                    maxlength="25"
                    :class="{ error: showCharacterError }"
                    v-model="array.cardholder"
                    type="text"
                /><br />
            </div>
            <section>
                <div>
                    <p>valid thru</p>
                    <input v-model="array.expireMonth" type="month" /><br />
                </div>
                <div>
                    <p>ccv</p>
                    <input maxlength="3" v-model="array.CCV" type="text" />
                </div>
            </section>
            <div>
                <p>vendor</p>
                <select v-model="array.vendor" type="options">
                    <option></option>
                    <option value="bitcoin">Bitcoin Inc</option>
                    <option value="blockchain">Blockchain Inc</option>
                    <option value="evil">Evil Corp</option>
                    <option value="ninja">Ninja Bank</option>
                </select>
                <br />
            </div>
            <p v-if="showCharacterError" class="error">
                Card holder field must only contain letters.
            </p>
            <p v-if="showDuplicateError" class="error">
                You alredy have this card number registerd.
            </p>
            <p v-if="showNumberError" class="error">
                Card number field must only contain numbers and 16 of them.
            </p>
            <p v-if="showError" class="error">
                Please fill all the text field.
            </p>
            <button @click="sendData">add card</button>
        </form>
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
            showError: false,
            showNumberError: false,
            showDuplicateError: false,
            showCharacterError: false,
        };
    },

    methods: {
        checkDuplicate() {
            let result = false;
            for (let card of this.cards) {
                if (Number(card.cardNumber) == Number(this.array.cardNumber)) {
                    result = true;
                }
            }
            return result;
        },
        checkLetterContains() {
            let characters = " abcdefghijklmnopqrstuvwxyzåäö";
            let splitted = this.array.cardholder.split("");
            let result = true;

            for (let i = 0; i < splitted.length; i++) {
                if (!characters.includes(splitted[i].toLowerCase())) {
                    result = false;
                }
            }

            return result;
        },

        sendData() {
            let numbers = Number(this.array.cardNumber);
            if (
                !this.array.cardNumber.length <= 0 &&
                !this.array.cardholder.length <= 0 &&
                !this.array.expireMonth.length <= 0 &&
                !this.array.CCV.length <= 0 &&
                !this.array.vendor.length <= 0
            ) {
                this.showError = false;
                if (!isNaN(numbers) && this.array.cardNumber.length == 16) {
                    this.showNumberError = false;

                    if (!this.checkDuplicate()) {
                        this.showDuplicateError = false;

                        if (this.checkLetterContains()) {
                            this.showCharacterError = false;
                            this.$emit("resivedData", this.array);
                            this.$emit("changeView");
                        } else {
                            this.showCharacterError = true;
                        }
                    } else {
                        this.showDuplicateError = true;
                    }
                } else {
                    this.showNumberError = true;
                }
            } else {
                this.showError = true;
                if (!isNaN(numbers) && this.array.cardNumber.length == 16) {
                    this.showNumberError = false;
                    if (!this.checkDuplicate()) {
                        this.showDuplicateError = false;
                        if (this.checkLetterContains()) {
                            this.showCharacterError = false;
                        } else {
                            this.showCharacterError = true;
                        }
                    } else {
                        this.showDuplicateError = true;
                    }
                } else {
                    this.showNumberError = true;
                }
            }
        },
    },
    components: {
        Card,
    },
    props: ["cards"],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.add-card {
    border: 1px solid black;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 414px;
    height: 896px;
    background-color: whitesmoke;
    a {
        position: absolute;
        border: 1px solid steelblue;
        color: steelblue;
        padding: 0.15rem 0.4rem;
        cursor: pointer;
    }
    a:hover {
        background-color: steelblue;
        color: white;
    }
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
        p.error {
            color: red;
        }
        input.error {
            border: 1px solid red;
        }
    }
}
</style>
