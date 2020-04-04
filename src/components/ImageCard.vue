<template>
  <li class="image-card">
    <img class="image-card__image" :src="image.url_n" :alt="image.title" />
    <div class="image-card__container">
      <p v-if="image.title" class="image-title">
        {{ shortString(image.title) }}
      </p>
      <p v-else class="image-title">No Title Found</p>
      <p class="image-owner">By {{ image.ownername }}</p>
      <section class="image-date-views-container">
        <p class="image-date">{{ image.datetaken }}</p>
        <p class="image-views">Views: {{ image.views }}</p>
      </section>
    </div>
  </li>
</template>

<script>
export default {
  name: "ImageCard",
  props: ["image"],
  methods: {
    shortString(string) {
      let trimString = (string, length) => {
        return string.length > length
          ? string.substring(0, length) + "..."
          : string;
      };
      return trimString(string, 15);
    }
  }
};
</script>

<style lang="scss" scoped>
.image-card {
  list-style: none;
  border-radius: 10px;
  overflow: hidden;
  transition: 0.5s ease-in-out;
  &:hover {
    cursor: pointer;
    box-shadow: 0px 0px 20px 3px rgba(177, 177, 177, 0.8);
    transition: 0.5s ease-in-out;
  }
}

.image-card__image {
  object-fit: cover;
  width: 100%;
  height: 250px;
}
.image-card__container {
  background-color: #fff;
}
.image-title {
  font-size: 16px;
  font-weight: 700;
  text-align: left;
  padding: 10px;
}
.image-owner {
  font-size: 14px;
  color: grey;
  text-align: left;
  padding: 0px 10px;
}
.image-date-views-container {
  color: #b3b3b3;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  font-size: 12px;
  margin-top: 20px;
  border-top: 1px solid lightgrey;
  padding: 10px;
  font-weight: 600;
}
</style>
