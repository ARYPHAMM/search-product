<template>
  <div>
    <Item :title="title" :root="root" v-for="item in items" :key="item.id" :item="item"/>
  </div>
</template>

<script>
import Item from "./Item.vue";
export default {
  name: "ListItems",
  props:['items','root','title'],
  components: {
    Item,
  },
};
</script>

<style></style>
