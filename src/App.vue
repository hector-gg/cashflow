<template>
    <Suspense>
        <template #default>
            <Home />
        </template>
        <template #fallback>
            <Splashscreen />
        </template>
    </Suspense>

    <Home />
</template>

<script>
import Splashscreen from "./components/Splashscreen.vue";
import { defineAsyncComponent } from "vue";

export default {
    components: {
        Splashscreen,
        Home: defineAsyncComponent(
            () =>
                new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(import("./components/Home"));
                    }, 2500);
                })
        ),
    },
};
</script>

<style>
html,
body,
.app {
    min-height: 100vh;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}
* {
    --brand-green: #04b500;
    --brand-blue: #0689b0;
}
</style>
