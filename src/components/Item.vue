<template>
  <div class="card d-flex flex-md-row mb-1">
    <div class="col-lg-2 col-12 p-lg-0">
      <img class="card-img-top" :src="thumbnail" alt="" />
    </div>
    <div class="col-lg-10 col-12 p-lg-0">
      <div class="card-body">
        <a :href="url" class="card-title text-primary" v-html="titleHightlight"></a>
        <div class="card-text">
          <p class="m-0">
            <b class="pr-1">Tình trạng:</b>
            <span class="text-success" v-if="item.status > 0">
              Còn hàng
            </span>
            <span class="text-danger" v-else>
              Hết hàng
            </span>
          </p>
          <p class="m-0">
            <b class="pr-1">Giá gốc:</b
            ><span class="text-danger">{{ price }}</span>
          </p>
          <p class="m-0">
            <b class="pr-1">Giá bán:</b
            ><span class="text-danger">{{ priceSale }}</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Item",
  props: ["item", "root","title"],
  computed: {
    price() {
      var price = this.item.price;
      return price == ""
        ? "Liên hệ"
        : parseInt(price).toLocaleString("it-IT", {
            style: "currency",
            currency: "VND",
          });
    },
    priceSale() {
      var price_sale = this.item.price_sale;
      return price_sale == ""
        ? "Liên hệ"
        : parseInt(price_sale).toLocaleString("it-IT", {
            style: "currency",
            currency: "VND",
          });
    },
    thumbnail() {
      return this.root + "/" + this.item.thumbnail;
    },
    url() {
      return this.root + "/" + this.item.uri + ".html";
    },
    titleHightlight() {
      console.log(this.title);
      var re = new RegExp(this.title, "gi");
      //  return this.item.title.replace(re,  function(str) { return "<span class='highlight'>"+str+"</span>" }); // #1
       return this.item.title.replace(re, "<span class='highlight'>$&</span>"); //#2
    },
  },
 
};
</script>
