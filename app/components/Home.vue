<template>
  <Page>
    <ActionBar>
      <Label text="Home" />
    </ActionBar>

    <GridLayout>
      <Button @tap="tapped" text="TEST" />
    </GridLayout>
  </Page>
</template>

<script lang="ts">
var Star = require("nativescript-print-star");
import Vue from "nativescript-vue";

export default Vue.extend({
  methods: {
    tapped(args) {
      console.log("Button was pressed");
      new Star.Discovery().searchBluetoothLE().catch((err) => {
        console.log(err);
      });
    },
  },
  computed: {
    message() {
      return "Blank {N}-Vue app";
    },
  },
});
</script>


