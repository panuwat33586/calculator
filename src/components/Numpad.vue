<template>
  <div class="row">
    <div
      v-for="(button, $buttonIndex) of buttons"
      :key="$buttonIndex"
      class="col-3"
    >
      <div class="button">
        <button
          type="button"
          class="btn btn-lg btn-primary"
          @click="sendButtonValue(button)"
        >
          {{ button }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Numpad",
  data() {
    return {
      buttons: [
        "C",
        "√",
        "%",
        "/",
        7,
        8,
        9,
        "*",
        4,
        5,
        6,
        "-",
        1,
        2,
        3,
        "+",
        0,
        ".",
        "=",
      ],
    };
  },
  methods: {
    sendButtonValue(value) {
      this.$emit("onButtonValue", value);
    },
  },
};
</script>

<style>
.button {
  margin: 5px;
}
</style>