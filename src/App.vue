<script setup>
import AOS from "aos";

import { onMounted, ref } from "vue";

import 'plyr/dist/plyr.css'


import FlipItem from "./components/FlipItem.vue";

const items = ref([
  {
    title: "Описание проекта",
    text: "Дизайн-код Бобровского сельского поселения – это уникальная система визуальной идентичности, которая подчёркивает природное богатство и культурное наследие региона. Основные элементы включают герб, фирменные цвета и паттерны, создающие цельный и узнаваемый образ поселения.",
    cover: "desc-long.jpg",
    image: "desc.jpg",
  },
  {
    title: "Герб посёлка Бобровский",
    text: "Герб отражает ключевые особенности территории: бобёр символизирует трудолюбие и созидание, деревья – лесные богатства и устойчивость, а река – важность водных ресурсов для жизни поселения. Цветовая гамма герба включает серебряный (чистота и гармония), зелёный (природа и развитие) и голубой (реки и ясное небо).",
    cover: "emblem-long.jpg",
    image: "emblem.jpg",
  },
  {
    title: "Цветовая гамма",
    text: `Основные цвета в дизайне отражают природу поселения: серебряный символизирует чистоту, зелёный – природные богатства, а голубой – реки. Дополнительные коричневый и золотой цвета подчеркивают лесное наследие и значимость территории.`,
    cover: "colors-long.jpg",
    image: "colors.jpg",
  },
  {
    title: "Паттерны и элементы",
    text: "Декоративные паттерны и элементы дизайна отражают природное и культурное наследие Бобровского. Органические формы вдохновлены местной флорой и пейзажами, геометрические узоры основаны на традиционных орнаментах, а текстуры передают атмосферу лесного и водного ландшафта. Элементы объединяются в гармоничный дизайн поселения.",
    cover: "patterns-long.jpg",
    image: "patterns.jpg"
  }
]);

onMounted(() => {

  AOS.init();

  // Common particle config for snowfall effect
  const snowConfig = {
    particles: {
      number: { value: 250 }, // Increased number of particles
      color: { value: '#457B9D' }, // White color for snow
      shape: {
        type: 'circle',
        stroke: { width: 0 }
      },
      size: {
        value: 3,
        random: true,
        min: 1,
        max: 5
      },
      move: {
        enable: true,
        speed: 1, // Slower speed
        direction: 'bottom',
        straight: false,
        out_mode: "out",
        random: true,
        bounce: false
      },
      opacity: {
        value: 0.8,
        random: true,
        min: 0.4,
        max: 0.8
      }
    }
  };

  // Initialize particles on both sides with snow config
  particlesJS('particles-left', snowConfig);
  particlesJS('particles-right', snowConfig);
});
</script>

<template>
  <div id="particles-left" class="particles-side particles-left"></div>
  <div id="particles-right" class="particles-side particles-right"></div>

  <main class="main">
    <h1 class="main-title">Дизайн-код посёлка Бобровский</h1>
    <p class="main-text">Бобровский – праздник начинается здесь!</p>
    <div class="main-rows">
      <div class="main-rows-item item" v-for="(item, i) in items" :data-aos="i % 2 === 0 ? 'fade-left' : 'fade-right'">
        <FlipItem :cover="item.cover" :image="item.image" />
        <div class="item-info">
          <h2 class="title-2 item-title">{{ item.title }}</h2>
          <p class="item-text" v-html="item.text" />
        </div>
      </div>
      <div class="item typography" data-aos="fade-right">
        <h2 class="title-2 item-title">Использованные шрифты</h2>
        <p class="item-text">
          В проекте используется шрифт Open Sans для основного текста и заголовков.
          Open Sans - современный шрифт без засечек, обеспечивающий отличную читаемость
          как в крупных заголовках, так и в мелком тексте.
        </p>
      </div>
    </div>
  </main>
  <footer class="footer">
    <p class="footer-copyright">
      Майнор "Иллюстрации на графическом планшете"
    </p>
    <p class="footer-date"> {{ new Date().getFullYear() }}. </p>
  </footer>
</template>

<style lang="scss" scoped>
.footer {
  margin-top: 5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.main {
  &-title {
    color: var(--green-color);
    text-align: center;
    font-size: 42px;
  }

  &-text {
    max-width: 768px;
    margin: 0 auto;
    text-align: center;
    color: var(--green-color);
    font-size: 24px;
  }

  &-rows {
    margin-top: 5rem;
    display: flex;
    flex-direction: column;
    gap: 5rem;

    &-item {
      height: 300px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2rem;

      &:nth-child(2n) {
        direction: rtl;
        text-align: left;
      }
    }
  }
}

.item {
  &-info {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  &-title {
    font-size: 32px;
    color: var(--green-color);
  }

  &-text {
    font-size: 18px;
  }
}

.typography {
  background: rgba(100, 149, 237, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 16px;
  padding: 2rem;
  border: 1px solid rgba(100, 149, 237, 0.2);
  box-shadow: 0 4px 30px rgba(100, 149, 237, 0.15);

  .item-title {
    margin-bottom: 1rem;
  }
}

.particles-side {
  position: fixed;
  top: 0;
  width: 150px;
  height: 100vh;
  z-index: -1;
}

.particles-left {
  left: 0;
}

.particles-right {
  right: 0;
}

@media (max-width: 1000px) {
  .footer {
    margin-top: 2rem;
    font-size: 14px;
    align-items: flex-end;
  }

  .main {
    &-title {
      font-size: 24px;
      text-align: left;
    }

    &-text {
      font-size: 18px;
      text-align: left;
    }

    .item-info {
      gap: .5rem;
    }

    .item-title {
      font-size: 18px;
    }

    .item-text {
      font-size: 14px;
    }


    &-rows {
      margin-top: 2rem;
      gap: 3rem;

      &-item {
        grid-template-columns: 1fr;
        height: auto;

        .plyr,
        img {
          height: 500px;
        }
      }
    }
  }

  .typography {
    padding: 1.5rem;
  }

  .particles-side {
    width: 50px;
  }
}
</style>
