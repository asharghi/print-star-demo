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
import {
  check as permissionCheck,
  request as requestPermission,
} from "@nativescript-community/perms";

export default Vue.extend({
  methods: {
    async checkAndAskForPermissions() {
      const comp = this;

      const isAuthorized = (response) => {
        if (Array.isArray(response)) return response.includes("authorized");
        else if (typeof response === "object" && response !== null)
          return Object.values(response).some(
            (value) => value === "authorized"
          );
        return false;
      };

      const bluetoothResponse = await permissionCheck("bluetooth");
      if (!isAuthorized(bluetoothResponse)) {
        await requestPermission("bluetooth");
      }

      return true;
    },
    tapped(args) {
      console.log("Button was pressed");

      this.checkAndAskForPermissions().then(() => {
        try {
          new Star.Discovery()
            .searchBluetoothLE()
            .then((res) => {
              console.log(res);
              console.log("Success");
            })
            .catch((err) => {
              console.log("-error");
              console.log(err);
            });
        } catch (error) {
          console.log("--error");
          console.log(error);
        }
      });
    },
  },
});
</script>


