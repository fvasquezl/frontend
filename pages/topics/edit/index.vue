<template>
  <div class="container">
    <h2>Update Topic Title</h2>

    <form @submit.prevent="update">
      <div class="form-goup mt-5">
        <input type="text" class="form-control" v-model="topic.title" />
        <small v-if="errors.title" class="form-text text-danger">{{errors.title[0]}}</small>
      </div>
      <button class="mt-2 btn btn-outline-success">Update</button>
    </form>

    <p class="mt-5 btn btn-outline-warning">
      <nuxt-link to="/topics">Back to Topics</nuxt-link>
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      topic: {
        title: ""
      }
    };
  },
  async asyncData({ $axios, params }) {
    const { data } = await $axios.$get(`topics/${params.id}`);
    return { topic: data };
  },
  methods: {
    async update() {
      await this.$axios.patch(`/topics/${this.$route.params.id}`, {
        title: this.topic.title
      });
      //redirect
      this.$router.push("/topics");
    }
  }
};
</script>

<style lang="scss" scoped>
</style>