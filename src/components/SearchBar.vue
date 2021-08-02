<template>
  <form action="POST">
      <div class="form-group mt-1">
        <div class="d-flex">
        <input  @input="name = $event.target.value;handleInput()" v-model="name" placeholder="..." type="text" class="form-control" name="" id="" aria-describedby="helpId" >
        </div>
        <small id="helpId" class="form-text text-muted">Nhập tên sản phẩm bạn cần tra cứu</small>
      </div>
  </form>
</template>

<script>
export default {
  name: "SearchBar",
  data(){
      return {
          name:''
      }
  },
  methods: {
      handleInput(){
          this.$emit('handleInput',this.name);
      }
  },
};
</script>

<style>
</style>
