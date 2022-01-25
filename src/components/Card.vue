<template>
    <article :class="['card', array.vendor]">
        <section>
            <div>
                <img src="../assets/wifi.svg" alt="" />
                <img src="../assets/chip.svg" alt="" />
            </div>
            <div>
                <img
                    v-if="array.vendor"
                    :src="require('../assets/' + array.vendor + '.svg')"
                    alt=""
                />
            </div>
        </section>
        <section>
            <h2 v-if="array.cardNumber <= 0">xxxx xxxx xxxx xxxx</h2>
            <h2>
                {{ cardNumberSpaced }}
            </h2>
        </section>
        <section>
            <div>
                <p>cardholder name</p>
                <h3 v-if="array.cardholder <= 0">Mynameis Jeff</h3>
                <h3>
                    {{ array.cardholder }}
                </h3>
            </div>
            <div>
                <p>Valid thru</p>
                <h3 v-if="array.expireMonth <= 0">0000/00</h3>
                <h3>
                    {{ array.expireMonth }}
                </h3>
            </div>
        </section>
    </article>
</template>

<script>
export default {
    props: ["array"],
    computed: {
        cardNumberSpaced() {
            return (
                this.array.cardNumber.slice(0, 4) +
                " " +
                this.array.cardNumber.slice(4, 8) +
                " " +
                this.array.cardNumber.slice(8, 12) +
                " " +
                this.array.cardNumber.slice(12, 16)
            );
        },
    },
};
</script>

<style scoped lang="scss">
.card {
    background-color: #d0d0d0;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    height: 210px;
    border-radius: 8px;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
.bitcoin {
    background-color: #ffae34;
}
.blockchain {
    background-color: #8b58f9;
}
.evil {
    background-color: #f33355;
}
.ninja {
    background-color: #222222;
    color: white;
}

.card section {
    display: flex;
    justify-content: space-between;
}

.card section div {
    display: flex;
    flex-direction: column;
}
.card section:nth-of-type(2) {
    display: flex;
    justify-content: center;

    h2 {
        font-weight: normal;
        font-size: 28px;
        font-family: "PT Mono", monospace;
    }
}
.card section:nth-of-type(3) {
    div {
        align-items: flex-start;
        p {
            padding: 0;
            margin: 0;
        }
        h3 {
            font-family: "PT Mono", monospace;
            padding: 0;
            margin: 0;
            font-weight: normal;
        }
    }
}
</style>
