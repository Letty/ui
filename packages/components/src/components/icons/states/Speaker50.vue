<template>
  <svg xmlns="http://www.w3.org/2000/svg" :width="size" :height="size / 1.3" viewBox="0 0 24.8 21">
    <g
      stroke="none"
      stroke-width="1"
      fill="none"
      fill-rule="evenodd"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <g :stroke="color">
        <path
          d="M5.5,7.5H2C1.2,7.5,0.5,8.2,0.5,9v3c0,0.8,0.7,1.5,1.5,1.5h3.5l7,7v-20L5.5,7.5L5.5,7.5z"
        />
        <path d="M17.5,4.5c1.7,1.4,3,3.7,3,6c0,2.3-1.3,4.6-3,6" />
        <path d="M15.5,7c1.1,0.8,2,2,2,3.5s-0.9,2.7-2,3.5" />
      </g>
    </g>
  </svg>
</template>

<script>
export default {
  props: {
    size: {
      type: Number,
      default: 23
    },
    color: {
      type: String,
      default: 'currentColor'
    }
  }
}
</script>
