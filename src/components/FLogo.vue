<template>
  <img class="f-logo" :src="Logo" d :style="logoStyle" alt="赞赞" />
</template>

<script lang="ts">
export default {
  name: 'FLogo',
}
</script>

<script setup lang="ts">
import Logo from '~/assets/logo.svg'
const props = defineProps<{
  size?: number
}>()

defineEmits(['click'])

const logoStyle = computed(() => {
  if (props.size !== undefined && props.size >= 0) {
    return { width: `${props.size}px`, height: `${props.size}px` }
  }
  return
})
</script>

<style>
.f-logo {
  width: 38px;
  height: 38px;
}
</style>
