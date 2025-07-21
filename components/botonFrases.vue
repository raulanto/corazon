<template>
    <div class="romantic-container">
        <button @click="mostrarFraseRomantica" class="romantic-button">
            Majo y Raul
        </button>
        <div v-if="fraseActual" class="frase-romantica">
            "{{ fraseActual }}"
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const frasesRomanticas = ref([
  "Eres el sueño que mi corazón no quiere dejar de soñar.",
  "Si te preguntan por mí, diles que me perdí en tus ojos y no quiero que me encuentren.",
  "El amor no se mira, se siente. Y yo cuando te veo, siento mariposas en mi alma.",
  "Eres la razón por la que mi corazón late más fuerte cada mañana.",
  "No necesito mirar las estrellas cuando tengo tu mirada iluminando mi vida.",
  "Si el amor fuera un viaje, yo querría perderme contigo para siempre.",
  "Eres la melodía que mi corazón repite en silencio todo el día.",
  "De todas las historias de amor, la mía favorita es la que estoy escribiendo contigo.",
  "No existe en el diccionario una palabra que defina lo que siento por ti.",
  "El mejor momento de mi día es cuando nuestros caminos se cruzan.",
  "Te amo mi princesa hermosa",
  "Eres mi Princesa hermosa",
  "Cada latido de mi corazón pronuncia tu nombre en silencio.",
  "Eres el sol que ilumina mis días más oscuros.",
  "Si el amor fuera poesía, tú serías el poema más hermoso jamás escrito.",
  "Contigo aprendí que el amor no tiene límites ni condiciones.",
  "Tu sonrisa es mi lugar favorito en todo el universo.",
  "Eres la dueña de mis pensamientos y la reina de mi corazón.",
  "Amar no es mirarse el uno al otro, es mirar juntos en la misma dirección... y yo quiero mirar siempre hacia ti.",
  "El verdadero amor no es otra cosa que el deseo inevitable de ayudar al otro para que sea quien es.",
  "Eres mi pensamiento favorito al despertar y mi sueño más dulce al dormir.",
  "No necesito magia para ser feliz, me basta con tenerte a ti.",
  "El amor más grande no es el que te hace llorar, sino el que seca tus lágrimas.",
  "Eres mi hoy y todos mis mañanas.",
  "Si pudiera darte algo en la vida, me gustaría darte la capacidad de verte a través de mis ojos. Solo entonces te darías cuenta de lo especial que eres para mí.",
  "No importa el lugar ni la hora, mi corazón siempre te encontrará.",
  "Eres mi persona favorita en este mundo y en todos los que puedan existir.",
  "El amor no es cuánto tiempo pasamos juntos, sino cuán bien vivimos ese tiempo.",
  "Prefiero pasar un minuto contigo que toda la eternidad sin ti.",
  "Eres la nota perfecta en la melodía de mi vida.",
  "No existe fuerza más poderosa en el mundo que el amor de una persona sincera.",
  "El amor verdadero no tiene final feliz, porque simplemente no tiene final.",
  "Eres mi refugio seguro en este mundo loco.",
  "Si tuviera que elegir entre respirar o amarte, usaría mi último aliento para decirte que te amo.",
  "El amor no es encontrar a alguien perfecto, sino ver perfectamente a alguien imperfecto.",
  "Eres mi paraíso en la tierra.",
  "Amar es encontrar en la felicidad de otro tu propia felicidad.",
  "No hay prisa en este mundo que valga más que un momento contigo.",
  "Eres la respuesta a todas las oraciones que nunca hice.",
  "El amor no necesita ser perfecto, solo necesita ser verdadero... y lo nuestro es tan real como la vida misma.",
  "Si el amor fuera un color, sería el color de tus ojos.",
  "Eres mi hoy, mi mañana y mi siempre.",
  "No hay distancia que pueda apagar el fuego de mi amor por ti.",
  "El amor más dulce es aquel que no se puede expresar con palabras.",
  "Eres mi pensamiento favorito y mi mejor realidad.",
  "Amar no es decir 'te amo' cada día, es demostrarlo en cada detalle.",
  "Si el amor tuviera forma, sería exactamente como tú.",
  "Eres la razón por la que creo en el destino.",
  "No hay medicina que cure lo que no cura la felicidad de verte.",
  "El verdadero amor es cuando dos almas se encuentran y reconocen que siempre estuvieron destinadas a estar juntas.",
  "Eres mi luz en la oscuridad, mi calma en la tormenta.",
  "Amar es descubrir que la felicidad no está en ser amado, sino en amar... y yo te amo con todo mi ser.",
  "Si el tiempo fuera eterno, querría pasarlo todo a tu lado.",
  "Eres mi mayor aventura y mi más dulce hogar.",
  "El amor no es cuestión de días, meses o años... es cuestión de latidos, y por ti mi corazón late más fuerte.",
  "No existe lugar en el mundo donde me sienta más completo que a tu lado.",
  "Eres mi sueño hecho realidad.",
  "Amar es encontrar en otro lo que nos completa, nos excita y nos da paz... y tú eres todo eso para mí.",
  "Si pudiera guardar momentos en frascos, el primero que guardaría sería el instante en que te conocí.",
  "Eres mi corazoncito de melón"
]);

const fraseActual = ref('');

const mostrarFraseRomantica = () => {
    const frasesDisponibles = frasesRomanticas.value.filter(frase => frase !== fraseActual.value);
    const indiceAleatorio = Math.floor(Math.random() * frasesDisponibles.length);
    fraseActual.value = frasesDisponibles[indiceAleatorio];
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&display=swap');

*{
    font-family: 'DM Serif Display', serif;
}


.romantic-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    padding: 20px;
    font-family: 'Arial', sans-serif;
}

.romantic-button {
    padding: 12px 24px;
    background-color: #ff6b81;
    color: white;
    border: none;
    border-radius: 25px;
    font-size: 16px;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.romantic-button:hover {
    background-color: #ff4757;
    transform: translateY(-2px);
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
}

.romantic-button:active {
    transform: translateY(1px);
}

.frase-romantica {
    padding: 15px 25px;
    background-color: #fff0f3;
    border-radius: 10px;
    max-width: 80%;
    text-align: center;
    font-style: italic;
    font-size: 18px;
    color: #333;
    animation: fadeIn 0.5s ease;
}
@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}





</style>