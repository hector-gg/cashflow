<template>
    <div>
        <svg
            @touchstart="tap"
            @touchmove="tap"
            @touchend="untap"
            viewBox="0 0 300 200"
        >
            <line
                stroke="#c4c4c4"
                stroke-width="2"
                x1="0"
                :y1="Zero"
                x2="300"
                :y2="Zero"
            />
            <polyline
                fill="none"
                stroke="#0689B0"
                stroke-width="2"
                :points="points"
            />
            <line
                v-show="showPointer"
                stroke="#04b500"
                stroke-width="2"
                :x1="pointer"
                y1="0"
                :x2="pointer"
                y2="200"
            />
        </svg>
        <p>Últimos 30 días</p>
    </div>
</template>

<script setup>
import { computed, defineProps, defineEmits, toRefs, ref, watch } from "vue";
const props = defineProps({
    amounts: {
        type: Array,
        default: () => [],
    },
});
const { amounts } = toRefs(props);

const amountToPixeles = (amount) => {
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);
    const amountAbs = amount + Math.abs(min);
    const minmax = Math.abs(max) + Math.abs(min);

    return 200 - ((amountAbs * 1) / minmax) * 200;
};

const Zero = computed(() => {
    return amountToPixeles(0);
});

const points = computed(() => {
    const total = amounts.value.length;
    return amounts.value.reduce((points, amount, i) => {
        const x = (300 / total) * (i + 1);
        const y = amountToPixeles(amount);
        return `${points} ${x},${y}`;
    }, `0,${amountToPixeles(amounts.value.length ? amounts.value[0] : 0)}`);
});

const showPointer = ref(false);
const pointer = ref(0);

const emit = defineEmits(["select"]);

watch(pointer, (value) => {
    const index = Math.ceil(value / (300 / amounts.value.length));
    if (index < 0 || index > amounts.value.length) return;
    emit("select", amounts.value[index - 1], index - 1);
});

const tap = ({ target, touches }) => {
    //targe: devuelve el elemento sobre el que estamos trabajando.
    //touches: de vuelve las coordenadas.
    showPointer.value = true;
    const elementWith = target.getBoundingClientRect().width;
    const elementX = target.getBoundingClientRect().x;
    const touchX = touches[0].clientX;
    pointer.value = ((touchX - elementX) * 300) / elementWith;
};

const untap = () => {
    showPointer.value = false;
};
</script>

<style scoped>
svg {
    width: 100%;
}

p {
    text-align: center;
}
</style>
