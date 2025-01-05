<script setup>
import AOS from "aos";
import Plyr from 'plyr';

import { onMounted, ref } from "vue";

import 'plyr/dist/plyr.css'


import FlipItem from "./components/FlipItem.vue";

const items = ref([
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
  const player = new Plyr('#player');


  AOS.init();
});
</script>

<template>
  <main class="main">
    <h1 class="main-title">Дизайн-код посёлка Бобровский</h1>
    <p class="main-text">Бобровский – праздник начинается здесь!</p>
    <div class="main-rows">
      <div class="main-rows-item item" data-aos="fade-left">
        <!-- <video id="player" src="/video.mp4" controls></video> -->
        <div class="item-info">
          <h2 class="title-2 item-title">Описание проекта</h2>
          <p class="item-text">Дизайн-код Бобровского сельского поселения – это уникальная система визуальной
            идентичности, которая подчёркивает природное богатство и культурное наследие региона. Основные элементы
            включают герб, фирменные цвета и паттерны, создающие цельный и узнаваемый образ поселения.</p>
        </div>
      </div>
      <div class="main-rows-item item" v-for="(item, i) in items" :data-aos="i % 2 === 0 ? 'fade-left' : 'fade-right'">
        <FlipItem :cover="item.cover" :image="item.image" />
        <div class="item-info">
          <h2 class="title-2 item-title">{{ item.title }}</h2>
          <p class="item-text" v-html="item.text" />
        </div>
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

    &-rows {
      margin-top: 2rem;
      gap: 3rem;

      &-item {
        grid-template-columns: 1fr;
        height: auto;

        .item-info {
          gap: .5rem;
        }

        .item-title {
          font-size: 18px;
        }

        .item-text {
          font-size: 14px;
        }

        .plyr,
        img {
          height: 500px;
        }
      }
    }
  }
}
</style>
