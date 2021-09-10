<template>
  <div>
    <div class="input-group mb-3">
      <input
        type="text"
        class="form-control border-0"
        placeholder="Search..."
        aria-label="Recipient's username"
        aria-describedby="basic-addon2"
        v-model.trim="userTitle"
      />
      <span
        class="input-group-text border-0 bg-danger text-white"
        id="basic-addon2"
        @click="$emit('sendTitle', userTitle)"
        >Search</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "Searchbar",
  data() {
    return {
      userTitle: "",
    };
  },
};
</script>

<style style="scss" scoped>
</style>