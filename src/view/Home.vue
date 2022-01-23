<template>
    <div class="home">
        <a v-if="isEdit" @click="isEdit = false" class="done">Done</a>
        <a v-else @click="isEdit = true" class="edit">Edit</a>

        <h1>e-wallet</h1>
        <p>active card</p>
        <Card :array="current" />
        <br />
        <br />
        <div v-if="showModal" class="modal-container"></div>
        <div v-if="showModal" class="modal">
            <p>Are you sure?</p>
            <div>
                <button
                    @click="[(isEdit = false), (showModal = false)]"
                    class="cancel"
                >
                    Cancel
                </button>
                <button
                    @click="
                        [
                            $emit('removeCard', arrayData),
                            (isEdit = false),
                            (showModal = false),
                            (current = cards[0]),
                        ]
                    "
                    class="confirm"
                >
                    Confirm
                </button>
            </div>
        </div>
        <div class="cards-list">
            <a
                class="list-item"
                @click="change(array)"
                v-for="array in cards"
                :key="array.cardNumber"
            >
                <a
                    v-if="isEdit"
                    @click="[(showModal = true), (arrayData = array)]"
                >
                    <div>
                        <img src="../assets/clear_black_24dp.svg" alt="" />
                    </div>
                </a>
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
            isEdit: false,
            showModal: false,
            arrayData: null,
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
    .edit,
    .done {
        position: absolute;

        border: 1px solid steelblue;
        color: steelblue;
        padding: 0.15rem 0.4rem;
        cursor: pointer;
    }
    .edit .done:hover {
        background-color: steelblue;
        color: white;
    }
    .modal-container {
        z-index: 100;
        position: absolute;
        width: 414px;
        height: 896px;
        background-color: black;
        opacity: 50%;
    }
    .modal {
        position: absolute;
        z-index: 150;
        left: 8%;
        top: 50%;
        border: 1px solid black;
        height: 200px;
        width: 300px;
        background-color: white;
        display: flex;
        flex-direction: column;
        justify-content: center;

        div {
            display: flex;
            justify-content: space-around;
            align-items: center;
        }
        .cancel {
            color: white;
            background-color: red;
        }
        .confirm {
            color: white;
            background-color: green;
        }
    }
}

.cards-list {
    display: flex;
    flex-direction: column;
    max-height: 400px;

    div {
        position: absolute;
        display: flex;
        transform: translateY(-50%);

        img {
            border: 1px solid #222;
            color: whitesmoke;
            border-radius: 50%;
            background-color: whitesmoke;
            padding: 0.2rem;
        }
    }
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
