<template>
  <div class="row">
    <div
      v-for="({button,append}, $buttonIndex) of buttons"
      :key="$buttonIndex"
      class="col-3"
    >
      <div class="button">
        <button
          type="button"
          class="btn btn-lg btn-primary"
          @click="append(button)"
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
        {button:"C",append:this.appendOperation},
        {button:"√",append:this.appendOperation},
        {button:"%",append:this.appendOperation},
        {button:"/",append:this.appendOperation},
        {button:7,append:this.appendNumber},
        {button:8,append:this.appendNumber},
        {button:9,append:this.appendNumber},
        {button:"*",append:this.appendOperation},
        {button:4,append:this.appendNumber},
        {button:5,append:this.appendNumber},
        {button:6,append:this.appendNumber},
        {button:"-",append:this.appendOperation},
        {button:1,append:this.appendNumber},
        {button:2,append:this.appendNumber},
        {button:3,append:this.appendNumber},
        {button:"+",append:this.appendOperation},
        {button:0,append:this.appendNumber},
        {button:".",append:this.appendNumber},
        {button:"=",append:this.appendOperation},
      ],
    };
  },
  methods: {
    appendNumber(value) {
      this.$emit("appendNumber", value);
    },
    appendOperation(operation){
      this.$emit("appendOperation",operation)
    }
  },
};
</script>

<style>
.button {
  margin: 5px;
}
</style>