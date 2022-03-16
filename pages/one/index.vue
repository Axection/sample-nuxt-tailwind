<template>
  <div>
    <h2 class="text-2xl leading-7 font-semibold">
      Card Generator
    </h2>
    <p class="mt-3 text-gray-600">
      A <span class="italic">state-of-the-art</span> Card Generator for general use.
      <br>
    </p>
    <div class="relative mt-3 text-gray-600">
      <div v-if="isLoading" class="absolute left-0 top-0 w-full h-full bg-black bg-opacity-20 flex justify-center items-center">
        <simple-spinner />
      </div>
      <div class="inp-container">
        <label class="inp-label" for="id">ID</label>
        <input v-model="cardContents.id" class="inp-form" name="id" type="text" readonly size="5">
      </div>
      <div class="inp-container">
        <label class="inp-label" for="card-name">Name</label>
        <input v-model="cardName" class="inp-form" name="card-name" type="text">
      </div>
      <div class="inp-container">
        <label class="inp-label" for="card-name">Caption</label>
        <input v-model="cardContents.caption" class="inp-form" name="caption" type="text">
      </div>
      <div class="inp-container">
        <label class="inp-label" for="card-from">Sender Name</label>
        <input v-model="cardContents.from" class="inp-form" name="card-from" type="text">
      </div>
      <div class="inp-container">
        <label class="inp-label" for="card-to">Recipient Name</label>
        <input v-model="cardContents.to" class="inp-form" name="card-to" type="text">
      </div>

      <p class="border-t border-dashed mt-4" />
      <h3 class="text-xl leading-7 font-semibold">
        Preview
      </h3>
      <p class="pt-4 text-gray-800 ">
        To get started, remove
        <code class="bg-gray-100 text-sm p-1 rounded border">components/Tutorial.vue</code>
        and start coding in
        <code class="bg-gray-100 text-sm p-1 rounded border">pages/index.vue</code>. Have fun!
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import SimpleSpinner from "~/components/SimpleSpinner.vue";
export default Vue.extend({
  components: { SimpleSpinner },
  data() {
    return {
      isLoading: true,
      cardName: "Example",
      cardContents: {
        caption: "Your text here",
        id: 0,
      }
    };
  },
  async mounted() {
    const cardContents = await this.fetchContent();
    this.cardContents = cardContents;
    this.isLoading = false;
  },
  methods: {
    /** Mock endpoint load */
    fetchContent() {
      const contentData = {
        id: 3279,
        caption: "Wish you were here!",
        from: "Sisca",
        to: "Aditya",
      };
      return new Promise<typeof contentData>(resolve => setTimeout(() => resolve(contentData), 1500));
    }
  }
});
</script>

<style scoped>
.inp-label {
  @apply border-b-2 border-dotted
}
.inp-form {
  @apply rounded-md px-1 py-2 border-solid border-green-300 bg-gray-100
}

.inp-container {
  @apply rounded-md border-solid my-2
}
</style>
