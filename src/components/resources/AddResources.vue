<template>
  <base-dialog
    v-if="InputIsInvalid"
    title="Input Invalid"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortuantely, atleast one of the input value is invalid</p>
      <p>Please fill all the input field</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input ref="titleInput" id="title" name="title" type="text" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          row="3"
          ref="descIput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="Link">Link</label>
        <input ref="linkInput" id="Link" name="Link" type="url" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
  data() {
    return {
      InputIsInvalid: false,
    };
  },
  inject: ['addResource'],
  methods: {
    submitData() {
      //   console.log('title\n\n\\n\n\n', this.title, this.description, this.link);
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descIput.value;
      const enteredURL = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredURL.trim() === ''
      ) {
        this.InputIsInvalid = true;
        return;
      }

      this.addResource(enteredTitle, enteredDescription, enteredURL);
    },
    confirmError() {
      this.InputIsInvalid = false;
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
