<template>
  <Page>
    <ActionBar>
      <Label text="NativeScript Issues tests" />
    </ActionBar>

    <GridLayout @layoutChanged="updateLayout" rows="auto, *" :columns="columns">
      <StackLayout padding="15">
        <Label>Server Url</Label>
        <TextField keyboardType="url" v-model="serverUrl" />
        <label>You entered :: {{ serverUrl }}</label>
      </StackLayout>

      <GridLayout row="1">
        <StackLayout>
          <ListView height="100%" for="item in items">
            <v-template>
              <GridLayout
                paddingTop="10"
                paddingBottom="10"
                class="message bg-main t-14"
                paddingLeft="15"
                paddingRight="15"
                rows="auto"
                columns="auto, *"
              >
                <StackLayout class="v-center" col="1" paddingLeft="10">
                  <GridLayout columns="*, auto, auto" orientation="horizontal">
                    <Label class="t-16 font-bold">{{ item }} {{ item }}</Label>
                    <Label col="1" marginLeft="10" class="t-12 text-gray">{{
                      item
                    }}</Label>

                    <StackLayout
                      marginLeft="10"
                      col="2"
                      width="12"
                      height="12"
                      borderRadius="12"
                    ></StackLayout>
                  </GridLayout>

                  <Label class="t-15">{{ item }}</Label>
                </StackLayout>
              </GridLayout>
            </v-template>
          </ListView>
        </StackLayout>
      </GridLayout>

      <Label row="1" col="1">Landscape</Label>
    </GridLayout>
  </Page>
</template>

<script>
import AlertIcon from "./AlertIcon.vue";
import { screen } from "@nativescript/core/platform";

export default {
  components: {
    AlertIcon,
  },

  data() {
    return {
      columns: "*, 0",
      loading: false,
      serverUrl: "",
      items: Array(400)
        .fill(1)
        .map((i) => i + 1),
    };
  },

  mounted() {
    this.loading = true;

    setTimeout(() => {
      this.loading = false;
    }, 300);
  },

  methods: {
    updateLayout() {
      const width = screen.mainScreen.widthDIPs;
      console.log(width);

      console.log("*********** LAYOUT WIDTH", width);

      if (width < 1000) {
        this.columns = "*, 0";
      } else {
        this.columns = "400, *";
      }

      console.log(this.columns);

      this.$nextTick(() => {
        this.$forceUpdate();
      });
    },
  },
};
</script>

<style scoped lang="scss">
@import "@nativescript/theme/scss/variables/blue";

// Custom styles
.fas {
  @include colorize($color: accent);
}

.info {
  font-size: 20;
  horizontal-align: center;
  vertical-align: center;
}
</style>
