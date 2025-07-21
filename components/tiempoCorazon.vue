<template>
    <div class="">
        <div v-if="timePassed" class="w-full font-serif">
            <p class=" text-shadow-md text-rose-500">
                <span class="text-xs sm:text-base md:text-xl"> Han pasado: </span>
                <samp
                    class=" text-4xl sm:text-6xl md:text-8xl font-bold font-serif text-shadow-md">{{
                    timePassed.days }}</samp>
                <span class="text-xs sm:text-base md:text-xl"> días, </span>

                <samp
                    class=" text-4xl sm:text-6xl md:text-8xl font-bold font-serif text-shadow-md">{{
                    timePassed.hours }}</samp>
                <span class="text-xs sm:text-base md:text-xl"> horas, </span>
                <samp
                    class=" text-4xl sm:text-6xl md:text-8xl font-bold font-serif text-shadow-md">{{
                    timePassed.minutes }}</samp>
                <span class="text-xs sm:text-base md:text-xl"> min, </span>
                <samp
                    class=" text-4xl sm:text-6xl md:text-8xl font-bold font-serif text-shadow-md">{{
                    timePassed.seconds }}</samp>
                <span class="text-xs sm:text-base md:text-xl"> seg, </span>
            </p>

            <section
                class="flex w-full justify-center items-center  text-shadow-md text-rose-500">
                <span class=" text-4xl sm:text-6xl md:text-8xl font-bold font-serif">{{ timeAdosMeses.years
                    }}</span>
                años,
                <span class=" text-4xl sm:text-6xl md:text-8xl font-bold font-serif">{{ timeAdosMeses.months
                    }}</span>
                meses,
            </section>
        </div>
        <div v-else>
            <p>El 26 de Octubre de 2024 aún no ha llegado</p>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from "vue";

const timePassed = ref(null);
const timeAdosMeses = ref(null);
const timer = ref(null);

const targetDate = computed(() => {
    // 26 de Octubre de 2024 (meses van de 0 a 11)
    return new Date(2024, 9, 26);
});

const calculateTimePassed = () => {
    const now = new Date();
    const target = targetDate.value;

    if (now > target) {
        const diff = now - target; // diferencia en milisegundos

        // Calcular días, horas, minutos y segundos
        const days = Math.floor(diff / (1000 * 60 * 60 * 24));
        const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
        const seconds = Math.floor((diff % (1000 * 60)) / 1000);

        timePassed.value = { days, hours, minutes, seconds };
    } else {
        timePassed.value = null;
    }
};

const calculateAdsMeses = () => {
    const now = new Date();
    const target = targetDate.value;

    if (now > target) {
        // Calculamos la diferencia total en milisegundos
        const diff = now - target;

        // Cálculo preciso de años, meses y días
        let years = now.getFullYear() - target.getFullYear();
        let months = now.getMonth() - target.getMonth();
        let days = now.getDate() - target.getDate();

        // Ajustamos si los días son negativos
        if (days < 0) {
            const lastMonth = new Date(now.getFullYear(), now.getMonth(), 0);
            days += lastMonth.getDate();
            months--;
        }

        // Ajustamos si los meses son negativos
        if (months < 0) {
            months += 12;
            years--;
        }

        // Calculamos horas, minutos y segundos
        const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
        const seconds = Math.floor((diff % (1000 * 60)) / 1000);

        timeAdosMeses.value = {
            years,
            months,
            days,
            hours,
            minutes,
            seconds,
        };
    } else {
        timeAdosMeses.value = null;
    }
};

onMounted(() => {
    // Calcular inmediatamente
    calculateTimePassed();
    calculateAdsMeses();
    // Actualizar cada segundo (1000 ms)
    timer.value = setInterval(calculateTimePassed, 1000);
});

onBeforeUnmount(() => {
    // Limpiar el intervalo cuando el componente se desmonte
    clearInterval(timer.value);
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&display=swap");

* {
    font-family: "DM Serif Display", serif;
}
</style>
