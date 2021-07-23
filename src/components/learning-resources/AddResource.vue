<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Atleast one input value is invalid!</p>
      <p>Please fill in all fields...</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" v-model="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" v-model="description" ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" v-model="link" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue'
import BaseCard from '../UI/BaseCard.vue'
export default {
  components: { BaseCard, BaseButton },
  inject: ['addResource'],
  data() {
    return {
      title: '',
      description: '',
      link: null,
      inputIsInvalid: false
    }
  },
  methods: {
    submitData() {
      if (this.title.trim() === '' || this.description.trim() === '' || this.link.trim() === '') {
        return this.inputIsInvalid = true;
      }

      this.addResource(this.title, this.description, this.link);
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
}
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