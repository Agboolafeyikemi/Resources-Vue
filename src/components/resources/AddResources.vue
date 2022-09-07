<template>
  <base-card>
    <form @submit.prevent="addResources">
      <div class="form-control">
        <label for="title">Title</label>
        <input :v-model="title" id="title" name="title" type="text" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          :v-model="description"
          id="description"
          name="description"
          row="3"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="Link">Link</label>
        <input :v-model="link" id="Link" name="Link" type="url" />
      </div>
      <div>
        <base-button :v-on="addResources" type="submit"
          >Add Resource</base-button
        >
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      description: '',
      link: '',
    };
  },
  methods: {
    addResources() {
      console.log('title\n\n\\n\n\n', this.title, this.description, this.link);
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
