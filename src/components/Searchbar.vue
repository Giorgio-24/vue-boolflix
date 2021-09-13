<template>
  <div>
    <div class="input-group mb-3">
      <input
        type="text"
        class="form-control border-0"
        :placeholder="placeholder"
        @keyup.enter="
          $emit('sendResearch', userResearch);
          $emit('newTemplate');
        "
        aria-label="Recipient's username"
        aria-describedby="basic-addon2"
        v-model.trim="userResearch"
      />
      <span
        class="input-group-text border-0 bg-danger text-white"
        id="basic-addon2"
        @click="
          $emit('sendResearch', userResearch);
          $emit('newTemplate');
        "
        >{{ buttonText }}</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "Searchbar",
  props: ["placeholder", "buttonText"],
  data() {
    return {
      userResearch: "",
    };
  },
};
</script>

<style style="scss" scoped>
</style>