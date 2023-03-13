<template>
  <div class="parallax">
    <svg width="30" height="30" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg">
      <path
        d="M468.97 115.03c-30.984-30.982-72.19-48.057-116.555-48.057-44.365 0-85.57 17.075-116.555 48.057L47.03 347.03c-30.981 30.984-48.057 72.189-48.057 116.554 0 44.365 17.076 85.57 48.057 116.555 30.984 30.983 72.189 48.057 116.554 48.057 44.366 0 85.57-17.074 116.555-48.057l305.942-305.941c30.983-30.983 48.057-72.19 48.057-116.555 0-44.365-17.074-85.57-48.057-116.554zm-39.06 77.692L189.616 385.97c-10.154 10.154-23.705 15.751-38.146 15.751s-28.992-5.597-39.146-15.751c-10.154-10.154-15.75-23.705-15.75-38.146s5.596-28.992 15.75-39.146L357.38 152.576c10.154-10.154 23.705-15.75 38.146-15.75s28.992 5.596 39.146 15.75c10.154 10.154 15.75 23.705 15.75 39.146s-5.596 28.992-15.75 39.146z"
        fill="#000" />
    </svg>

  </div>
</template>

<script>
export default {
  props: {
    speed: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {
      translateY: 0
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      const scrollTop = window.scrollY
    }
  }
}
</script>

<style lang="less">
.parallax {
  position: relative;
  overflow: hidden;
  height: 100vh;

  svg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transform: translateY(1);
  }
}</style>
