<template>
  <div class="home">
    <form>
      <label>
        Search:
        <input v-model="searchText" type="text" />
      </label>
      <button type="submit" class="go-button" @click.prevent="search">
        Search
      </button>
    </form>
    <p v-if="loading">Loading...</p>
    <ul v-else class="image-card-list">
      <image-card
        v-for="image in images"
        :key="image.id"
        :image="image"
      ></image-card>
    </ul>
  </div>
</template>

<script>
import HelloWorld from "@/components/HelloWorld.vue";
import API_KEY from "../../public/config";
import axios from "axios";
import config from "../../public/config";
import ImageCard from "@/components/ImageCard";

export default {
  name: "Home",
  components: {
    ImageCard
  },
  data() {
    return {
      searchText: "",
      loading: false,
      images: []
    };
  },
  methods: {
    search() {
      this.loading = true;
      console.log("Searching for: ", this.searchText);
      this.fetchImages().then(response => {
        console.log(response.data.photos.photo);
        this.images = response.data.photos.photo;
        this.loading = false;
      });
    },
    fetchImages() {
      return axios({
        method: "get",
        url: "https://api.flickr.com/services/rest",
        params: {
          method: "flickr.photos.search",
          api_key: config.API_KEY,
          tags: this.searchText,
          extras: "url_n, owner_name, date_taken, views",
          page: 1,
          format: "json",
          nojsoncallback: 1,
          per_page: 20
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.image-card-list {
  margin-top: 40px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-column-gap: 25px;
  grid-row-gap: 25px;
  @media only screen and (max-width: 1024px) {
    grid-template-columns: 1fr 1fr;
  }
  @media only screen and (max-width: 480px) {
    grid-template-columns: 1fr;
  }
}
</style>
