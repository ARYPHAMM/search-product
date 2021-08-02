<template>
  <div id="app">
    <div class="container">
      <div class="row flex-row-sm">
        <div class="col-lg-11 col-md-10 col-9">
          <SearchBar @handleInput="search" />
        </div>
        <div class="col-lg-1 col-md-2 col-3  mt-1">
          <input
            @input="handleInputLimit"
            v-model="limit"
            type="number"
            class="form-control input__limit"
            name=""
            id=""
            aria-describedby="helpId"
            placeholder=""
          />
          <small id="helpId" class="form-text text-muted text-limit"
            >hiển thị tối đa (mặc định 5)</small
          >
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <ListItems :title="title" :root="root_api" :items="items" v-if="items.length" />
          <div v-else v-show="display">
            <div class="text-center">
              Không tìm thấy kết quả
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import ListItems from "./components/ListItems.vue";
import axios from "axios";
const api = "https://pharmacyfull.com/ajax/getlist.php";
export default {
  name: "App",
  components: {
    SearchBar,
    ListItems,
  },
  data() {
    return {
      items: [],
      display: false,
      root_api: "https://pharmacyfull.com",
      limit: 5,
      title:'',
    };
  },
  methods: {
    search(title) {
      const data = new FormData();
      this.title = title;
      data.append("title", title);
      data.append("limit", this.limit <= 5 ? 5 : this.limit );
      axios.post(api, data).then((response) => {
        this.items = response.data;
        if (response.data == false && title != "") this.display = true;
        else this.display = false;
      });
    },
    handleInputLimit(){
      this.search(this.title);
    }
  },
};
</script>
