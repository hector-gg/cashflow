<template>
    <Layout>
        <template #header>
            <Header></Header>
        </template>

        <template #resume>
            <Resume
                :label="'Ahorro total'"
                :amount="amount"
                :total-amount="100000"
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
            movements: [
                {
                    id: 0,
                    title: "Movimiento 1",
                    description: "Deposito de salario",
                    amount: 100,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 1,
                    title: "Movimiento 2",
                    description: "Deposito de honorarios",
                    amount: 200,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 2,
                    title: "Movimiento 3",
                    description: "Comida",
                    amount: 500,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 3,
                    title: "Movimiento 4",
                    description: "Colegiatura",
                    amount: 200,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 4,
                    title: "Movimiento 5",
                    description: "Reparación equipo",
                    amount: -400,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 5,
                    title: "Movimiento 6",
                    description: "Reparación equipo",
                    amount: -600,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 6,
                    title: "Movimiento 7",
                    description: "Reparación equipo",
                    amount: -300,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 7,
                    title: "Movimiento 8",
                    description: "Reparación equipo",
                    amount: 100,
                    time: new Date("11-08-2023"),
                },
                {
                    id: 8,
                    title: "Movimiento 9",
                    description: "Reparación equipo",
                    amount: 300,
                    time: new Date("01-01-2023"),
                },
                {
                    id: 9,
                    title: "Movimiento 10",
                    description: "Reparación equipo",
                    amount: 500,
                    time: new Date("01-01-2023"),
                },
            ],
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
    },
    methods: {
        create(movement) {
            this.movements.push(movement);
        },
        remove(id) {
            const index = this.movements.findIndex((m) => m.id === id);
            this.movements.splice(index, 1);
        },
    },
};
</script>
