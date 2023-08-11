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
                <template #graphic> graphic </template>
                <template #action>
                    <Action />
                </template>
            </Resume>
        </template>

        <template #movements>
            <Movements :movements="movements" />
        </template>
    </Layout>
</template>
<script>
import Layout from "@/components/Layout.vue";
import Header from "@/components/Header.vue";
import Resume from "@/components/Resume/Index.vue";
import Movements from "@/components/Movements/Movements.vue";
import Action from "@/components/Action.vue";

export default {
    components: {
        Layout,
        Header,
        Resume,
        Movements,
        Action,
    },
    data() {
        return {
            amount: null,
            now: new Date(), //null,
            movements: [
                {
                    id: 0,
                    title: "Movimiento 0",
                    description: "Deposito de salario",
                    amount: "1000",
                },
                {
                    id: 1,
                    title: "Movimiento 1",
                    description: "Deposito de honorarios",
                    amount: "500",
                },
                {
                    id: 2,
                    title: "Movimiento 2",
                    description: "Comida",
                    amount: "-100",
                },
                {
                    id: 3,
                    title: "Movimiento 3",
                    description: "Colegiatura",
                    amount: "-1000",
                },
                {
                    id: 4,
                    title: "Movimiento 4",
                    description: "Reparación equipo",
                    amount: "1000",
                },
                {
                    id: 5,
                    title: "Movimiento 5",
                    description: "Reparación equipo",
                    amount: "1000",
                },
                {
                    id: 6,
                    title: "Movimiento 6",
                    description: "Reparación equipo",
                    amount: "1000",
                },
            ],
        };
    },
};
</script>
