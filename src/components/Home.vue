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
            />
        </template>
        <template #movements>
            <Movements />
        </template>
    </Layout>
</template>
<script>
import Layout from "@/components/Layout.vue";
import Resume from "@/components/Resume/Index.vue";
import Header from "@/components/Header.vue";
import Movements from "@/components/Movements.vue";

export default {
    components: {
        Layout,
        Header,
        Resume,
        Movements,
    },
    data() {
        return {
            amount: null,
            now: new Date(),
        };
    },
    computed: {},
};
</script>
