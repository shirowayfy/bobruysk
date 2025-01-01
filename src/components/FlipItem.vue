<style lang='scss' scoped>
.item-flip {
  position: relative;
  overflow: hidden;
  cursor: pointer;

  &-cover {
    position: absolute;
    left: 0;
    top: 0;

    transition: all .5s;

    &:hover {
      transform: scale(1.5);
      opacity: 0;
    }
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }
}
</style>

<template>
  <div class="item-flip">
    <img :src="`/${cover}`" alt="" class="item-flip-cover">
    <img :src="`/${image}`" alt="">
  </div>
</template>

<script>
export default {
  props: ['cover', 'image'],
};
</script>