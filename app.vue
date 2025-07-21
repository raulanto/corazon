<template>
  <div>
  <div class="containers">
    <nuxt-page/>
  </div>
  </div>
</template>




<script setup>
import { onMounted, onUnmounted } from 'vue';

onMounted(() => {
  // Crear elemento del cursor personalizado
  const customCursor = document.createElement('div');
  customCursor.className = 'custom-cursor';
  document.body.appendChild(customCursor);

  // Crear contenedor para corazones
  const heartsContainer = document.createElement('div');
  heartsContainer.className = 'hearts-container';
  document.body.appendChild(heartsContainer);

  // Variables para controlar la frecuencia de corazones
  let lastHeartTime = 0;
  const heartDelay = 100; // Milisegundos entre corazones

  const moveCursor = (e) => {
    // Mover el cursor personalizado
    customCursor.style.left = e.clientX + 'px';
    customCursor.style.top = e.clientY + 'px';

    // Crear corazones con cierto retraso para no saturar
    const now = Date.now();
    if (now - lastHeartTime > heartDelay) {
      createHeart(e.clientX, e.clientY);
      lastHeartTime = now;
    }
  };

  const createHeart = (x, y) => {
    const heart = document.createElement('div');
    heart.className = 'heart-trail';
    heart.style.left = x + 'px';
    heart.style.top = y + 'px';
    
    // Variación aleatoria en tamaño y opacidad
    const size = Math.random() * 10 + 5;
    heart.style.width = size + 'px';
    heart.style.height = size + 'px';
    heart.style.opacity = Math.random() * 0.5 + 0.3;
    
    heartsContainer.appendChild(heart);
    
    // Eliminar el corazón después de animarse
    setTimeout(() => {
      heart.remove();
    }, 1000);
  };

  document.addEventListener('mousemove', moveCursor);

  onUnmounted(() => {
    document.removeEventListener('mousemove', moveCursor);
    customCursor.remove();
    heartsContainer.remove();
  });
});
</script>


<style>
@tailwind base;
@tailwind components;
@tailwind utilities;



/* Estilos para el rastro de corazones */
.heart-trail {
  position: absolute;
  background-color: #ff6b8b;
  display: inline-block;
  transform: rotate(-45deg);
  animation: float-up 1s ease-out forwards;
  pointer-events: none;
}

.heart-trail:before,
.heart-trail:after {
  content: "";
  width: inherit;
  height: inherit;
  background-color: inherit;
  border-radius: 50%;
  position: absolute;
}

.heart-trail:before {
  top: -50%;
  left: 0;
}

.heart-trail:after {
  top: 0;
  left: 50%;
}

@keyframes float-up {
  0% {
    transform: rotate(-45deg) translateY(0) scale(1);
    opacity: 1;
  }
  100% {
    transform: rotate(-45deg) translateY(-100px) scale(0.3);
    opacity: 0;
  }
}

/* Estilo para el contenedor de ejemplo */
.containers {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #fff5f7;
  font-family: 'Arial', sans-serif;
  text-align: center;
}

h1 {
  color: #d23669;
  margin-bottom: 20px;
}

p {
  color: #ff6b81;
  font-size: 1.2em;
}

</style>