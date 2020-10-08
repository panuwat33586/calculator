<template>
  <div class="displayContainer">
    <div class="card">
      <div class="card-body">
        <div class="float-right">
          <p>{{ showdisplay }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Display",
  props: {
    showdisplay: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
.displayContainer {
  width: 100%;
}
</style>
