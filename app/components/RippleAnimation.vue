<template>
  <GridLayout>
    <Image
      src="res://white_circle"
      @loaded="circleObject = $event.object"
      :tintColor="tintColor"
      opacity="0"
      scaleX="0"
      scaleY="0"
      :width="width"
      :height="width"
      borderRadius="100%"
    />

    <Image
      src="res://white_circle"
      @loaded="circleObject1 = $event.object"
      :tintColor="tintColor"
      opacity="0"
      scaleX="0"
      scaleY="0"
      :width="width"
      :height="width"
      borderRadius="100%"
    />

    <Image
      src="res://white_circle"
      @loaded="circleObject2 = $event.object"
      :tintColor="tintColor"
      opacity="0"
      scaleX="0"
      scaleY="0"
      :width="width"
      :height="width"
      borderRadius="100%"
    />
  </GridLayout>
</template>

<script>
export default {
  props: {
    tintColor: { type: String, default: "red" },
    width: { type: String, default: "52" },
    animated: { type: Boolean, default: true },
  },
  data() {
    return {
      circleObject: null,
      circleObject1: null,
      circleObject2: null,
    };
  },

  mounted() {
    setTimeout(() => {
      this.checkAnimation();
    }, 100)
  },

  methods: {
    async checkAnimation() {
      if (
        !this.circleObject ||
        !this.circleObject1 ||
        !this.circleObject2 ||
        !this.animated
      ) {
        clearInterval(this.interval);
        return;
      }

      try {
        clearInterval(this.interval);
        this.interval = setInterval(() => {
          this.animate();
        }, 1250);

         this.animate()
      } catch (e) {
        // console.log(e);
      }
    },

    async animate() {
      this.circleObject.scaleX = 0;
      this.circleObject.scaleY = 0;

      this.circleObject1.scaleX = 0;
      this.circleObject1.scaleY = 0;

      this.circleObject2.scaleX = 0;
      this.circleObject2.scaleY = 0;

      this.circleObject.opacity = 1;
      this.circleObject1.opacity = 1;
      this.circleObject2.opacity = 1;

      try {
        await Promise.all([
          await this.circleObject.animate({
            duration: 800,
            scale: {
              x: 1,
              y: 1,
            },
            opacity: 0,
          }),

          await this.circleObject1.animate({
            delay: 200,
            duration: 800,
            scale: {
              x: 1,
              y: 1,
            },
            opacity: 0,
          }),

          await this.circleObject2.animate({
            delay: 400,
            duration: 800,
            scale: {
              x: 1,
              y: 1,
            },
            opacity: 0,
          }),
        ]);
      } catch (e) {
        // console.log(e);
      }
    },
  },

  destroyed() {
    clearInterval(this.interval);
  },

  watch: {
    animated: {
      immediate: false,
      handler() {
        this.checkAnimation();
      },
    },
  },
};
</script>