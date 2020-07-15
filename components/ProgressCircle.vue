<template>
  <svg
    :height="radius * 2"
    :width="radius * 2"
  >
    <circle
      :stroke="color"
      fill="#032541"
      :stroke-dasharray="circumference + ' ' + circumference"
      :style="{ strokeDashoffset }"
      :stroke-width="stroke"
      :r="normalizedRadius"
      :cx="radius"
      :cy="radius"
    />
  </svg>
</template>

<script>
export default {
  props: {
    radius: {
      type: Number,
      require: true,
      default: () => 25
    },
    progress: {
      type: Number,
      require: true,
      default: () => 10
    },
    stroke: {
      type: Number,
      require: true,
      default: () => 3
    }
  },
  data () {
    const normalizedRadius = this.radius - this.stroke * 2
    const circumference = normalizedRadius * 2 * Math.PI

    return {
      normalizedRadius,
      circumference
    }
  },
  computed: {
    color () {
      if (this.progress >= 70) {
        return 'green'
      } else if (this.progress > 30) {
        return 'yellow'
      } else {
        return 'red'
      }
    },
    strokeDashoffset () {
      return this.circumference - this.progress / 100 * this.circumference
    }
  }
}
</script>

<style>
  circle {
    transition: stroke-dashoffset 0.35s;
    transform: rotate(-90deg);
    transform-origin: 50% 50%;
  }
</style>
