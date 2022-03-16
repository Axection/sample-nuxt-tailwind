<template>
  <div class="relative">
    <div v-if="isLoading" class="absolute left-0 top-0 w-full h-full bg-black bg-opacity-20 flex justify-center items-center z-10">
      <simple-spinner />
    </div>
    <h2 class="text-2xl leading-7 font-semibold">
      Card Generator
    </h2>
    <p class="mt-3 text-gray-600">
      A <span class="italic">state-of-the-art</span> Card Generator for general use.
      <br>
    </p>
    <div class="relative mt-3 text-gray-600">
      <div class="flex justify-between flex-row-reverse">
        <div class="inp-container">
          <label class="inp-label" for="id">ID</label>
          <input v-model="cardContents.id" class="inp-form" name="id" type="text" readonly size="5">
        </div>
        <div class="inp-container">
          <label class="inp-label" for="card-name">Title</label>
          <input v-model="cardContents.name" class="inp-form" name="card-name" type="text">
        </div>
      </div>
      <p class="border-t border-dashed my-2" />
      <div class="inp-container">
        <label class="inp-label" for="card-name">Caption</label>
        <input v-model="cardContents.caption" class="inp-form" name="caption" type="text">
      </div>
      <div class="inp-container">
        <label class="inp-label" for="card-from">Sender Name</label>
        <input v-model="cardContents.sender" class="inp-form" name="card-from" type="text">
      </div>
      <div class="inp-container">
        <label class="inp-label" for="card-to">Recipient Name</label>
        <input v-model="cardContents.recipient" class="inp-form" name="card-to" type="text">
      </div>

      <p class="border-t border-dashed mt-4" />
      <h3 class="text-xl leading-7 font-semibold mb-2">
        Preview
      </h3>
      <div class="relative card-base mx-auto">
        <div class="w-2/3 ml-1 mt-1">
          <span class="text-white font-bold text-4xl"> {{ cardContents.caption }} </span>
        </div>

        <div class="absolute bottom-2 right-2 flex flex-col text-sm text-right">
          <span class="">From: {{ cardContents.sender }} </span>
          <span class="">To: {{ cardContents.recipient }} </span>
        </div>
      </div>
      <p class="pt-4 text-gray-800 text-center">
        <button class="rounded-lg border-solid border-2 border-green-300 px-4 py-2 font-semibold text-lg" @click="submit">
          Submit
        </button>
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import SimpleSpinner from "~/components/SimpleSpinner.vue";

type Payload = Record<string, any>;

export default Vue.extend({
  components: { SimpleSpinner },
  data() {
    return {
      isLoading: true,
      cardId: 0,
      cardContents: {
        name: "New untitled card",
      } as Payload,
    };
  },
  mounted() {
    this.fetchContent();
  },
  methods: {
    /** Mock endpoint load */
    async fetchContent() {
      const contentData = {
        id: 3279,
        caption: "Wish you were here!",
        from: "Sisca",
        to: "Aditya",
        extra: {
          price: 30000,
          color: "green",
        }
      };
      const response = await new Promise<typeof contentData>(resolve => setTimeout(() => resolve(contentData), 1500));
      this.cardContents = response;
      // filter out data
      this.cardContents.sender = response.from;
      this.cardContents.recipient = response.to;
      this.cardContents.caption = response.caption;
      this.cardId = response.id;
      this.isLoading = false;
    },
    submit() {
      // TODO: implementation
      console.log(this.cardId, this.cardContents);
      alert(`Project ${this.cardContents.name} is created with details:
        Sender: ${this.cardContents.sender}
        Recipient: ${this.cardContents.recipient}

        Message: ${this.cardContents.caption}
      `);
    }
  }
});
</script>

<style scoped>
.inp-label {
  @apply border-b-2 border-dotted
}
.inp-form {
  @apply rounded-md px-1 py-2 border-solid border-green-400 bg-gray-100
}

.inp-container {
  @apply rounded-md border-solid my-2
}

.card-base {
  width: 320px;
  height: 180px;
  @apply bg-green-200 rounded-xl border-0
}
</style>
