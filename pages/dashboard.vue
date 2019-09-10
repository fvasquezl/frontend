<template>
  <div class="container col-md-6 mt-5">
    <h2>Create a new topic</h2>
    <br />
    <form @submit.prevent="create">
      <div class="form-group">
        <label>
          <strong>Topic Title:</strong>
        </label>
        <input
          v-model.trim="form.title"
          type="text"
          class="form-control"
          placeholder="Enter topic title"
          autofocus
        />
        <small class="form-text text-danger" v-if="errors.title">{{errors.title[0]}}</small>
      </div>
      <div class="form-group">
        <label>
          <strong>Topic body:</strong>
        </label>
        <textarea class="form-control" v-model="form.body" rows="5"></textarea>
        <small class="form-text text-danger" v-if="errors.body">{{errors.body[0]}}</small>
      </div>

      <button type="submit" class="btn btn-primary">Create</button>
    </form>
  </div>
</template> 

<script>
export default {
  middleware: ["auth"],

  data() {
    return {
      form: { title: "", body: "" }
    };
  },
  methods: {
    async create() {
      await this.$axios.$post("/topics", this.form);
      this.$route.push("/");
    }
  }
};
</script>