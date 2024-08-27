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
      try {
       (new Star.Discovery().searchBluetooth())
        .then((res) => {
          console.log("Success");
        })
        .catch((err) => {
          console.log('-error');
          console.log(err);
        });
      } catch (error) {
        console.log('--error');
        console.log(error);
      }
    },
  },
  computed: {
    message() {
      return "Blank {N}-Vue app";
    },
  },
});
</script>


