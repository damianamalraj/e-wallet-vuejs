<template>
    <article :class="['card', card.vendor]">
        <section>
            <div>
                <img src="../assets/wifi.svg" alt="wifi" />
                <img src="../assets/chip.svg" alt="chip" />
            </div>
            <div>
                <img
                    v-if="card.vendor"
                    :src="require('../assets/' + card.vendor + '.svg')"
                    alt="brand"
                />
            </div>
        </section>
        <section>
            <h2 v-if="card.cardNumber <= 0">xxxx xxxx xxxx xxxx</h2>
            <h2>
                {{ cardNumberSpaced }}
            </h2>
        </section>
        <section>
            <div>
                <p>cardholder name</p>
                <h3 v-if="card.cardholder <= 0">Mynameis Jeff</h3>
                <h3>
                    {{ card.cardholder }}
                </h3>
            </div>
            <div>
                <p>Valid thru</p>
                <h3 v-if="card.expireMonth <= 0">MM/YY</h3>
                <h3 v-if="card.expireMonth">
                    {{ dateFormate }}
                </h3>
            </div>
        </section>
    </article>
</template>

<script>
export default {
    props: ["card"],
    computed: {
        cardNumberSpaced() {
            return (
                this.card.cardNumber.slice(0, 4) +
                " " +
                this.card.cardNumber.slice(4, 8) +
                " " +
                this.card.cardNumber.slice(8, 12) +
                " " +
                this.card.cardNumber.slice(12, 16)
            );
        },
        dateFormate() {
            return (
                this.card.expireMonth.slice(5, 7) +
                "/" +
                this.card.expireMonth.slice(2, 4)
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
