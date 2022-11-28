<template>
  <AbsoluteLayout
    :width="width"
    :height="width"
    class="panic-alert h-center v-center"
    padding="0"
  >
    <StackLayout :width="width" :height="width" class="out-circle-panic">
      <StackLayout class="image" :class="{ inverted: invertBg }">
        <Image
          src="res://alert_button"
          :width="imageWidth"
          :height="imageHeight"
          stretch="fill"
        />
      </StackLayout>
    </StackLayout>

    <ripple-animation :animated="true"></ripple-animation>
  </AbsoluteLayout>
</template>

<script>
import RippleAnimation from './RippleAnimation.vue';

export default {
  components: { RippleAnimation },
  props: {
    invertBg: {
      type: Boolean,
    },
    width: {
      type: Number,
      default: 52,
    },
    imageWidth: {
      type: Number,
      default: 25,
    },
    imageHeight: {
      type: Number,
      default: 29,
    },
    animated: {
      type: Boolean,
      default: false,
    },
    isDarkMode: {
      type: Boolean,
    },
  },
};
</script>