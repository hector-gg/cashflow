<template>
    <Layout>
        <template #header>
            <Header></Header>
        </template>

        <template #resume>
            <Resume
                :label="'Ahorro total'"
                :amount="amount"
                :total-amount="totalAmount"
                :date="now"
            >
                <template #graphic>
                    <Graphic :amounts="amounts" />
                </template>
                <template #action>
                    <Action @create="create" />
                </template>
            </Resume>
        </template>

        <template #movements>
            <Movements :movements="movements" @remove="remove" />
        </template>
    </Layout>
</template>
<script>
import Layout from "@/components/Layout.vue";
import Header from "@/components/Header.vue";
import Resume from "@/components/Resume/Index.vue";
import Movements from "@/components/Movements/Movements.vue";
import Action from "@/components/Action.vue";
import Graphic from "./Resume/Graphic.vue";

export default {
    components: {
        Layout,
        Header,
        Resume,
        Movements,
        Action,
        Graphic,
    },
    data() {
        return {
            amount: null,
            now: new Date(), //null,
            movements: [],
        };
    },
    computed: {
        amounts() {
            const lastDays = this.movements
                .filter((m) => {
                    const today = new Date();
                    const oldDate = today.setDate(today.getDate() - 30);
                    return m.time >= oldDate;
                })
                .map((m) => m.amount);

            return lastDays.map((m, i) => {
                const lastMovements = lastDays.slice(0, i);
                return lastMovements.reduce((suma, movement) => {
                    return suma + movement;
                }, 0);
            });
        },
        totalAmount() {
            return this.movements.reduce((suma, m) => {
                return suma + m.amount;
            }, 0);
        },
    },
    mounted() {
        const movements = JSON.parse(localStorage.getItem("movements"));

        if (Array.isArray(movements)) {
            this.movements = movements.map((m) => {
                return { ...m, time: new Date(m.time) };
            });
        }
    },
    methods: {
        create(movement) {
            this.movements.push(movement);
            this.save();
        },
        remove(id) {
            const index = this.movements.findIndex((m) => m.id === id);
            this.movements.splice(index, 1);
            this.save();
        },
        save() {
            localStorage.setItem("movements", JSON.stringify(this.movements));
        },
    },
};
</script>
