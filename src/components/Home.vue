<template>
    <Layout>
        <template #header>
            <Header></Header>
        </template>
        <template #resume>
            <Resume />
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
};
</script>
