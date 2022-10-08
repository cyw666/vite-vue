<script setup lang="ts">
import { Loading } from '@element-plus/icons-vue'
import type { ButtonHTMLAttributes } from 'vue'

const props = withDefaults(
  defineProps<{
    width?: string
    size?: string
    type?: string
    round?: boolean
    block?: boolean
    disabled?: boolean
    nativeType?: ButtonHTMLAttributes['type']
    loading?: boolean
  }>(),
  {
    size: 'default',
    type: 'default',
    round: false,
    block: false,
    disabled: false,
    nativeType: 'button',
    loading: false,
  }
)

const emit = defineEmits(['click'])

const handleClick = (evt: MouseEvent) => {
  emit('click', evt)
}
const styles = computed(() => {
  return props.width && { width: props.width }
})

const buttonRef = ref(null)
</script>

<template>
  <button
    ref="buttonRef"
    class="app-button"
    :class="[
      {
        'is-round': round,
        'is-block': block,
      },
      type ? `app-button--${type}` : null,
      size ? `app-button--${size}` : null,
      disabled ? 'app-button--disabled' : null,
      loading ? 'is-loading' : null,
    ]"
    :style="styles"
    :type="nativeType"
    :disabled="disabled"
    @click="handleClick"
  >
    <span class="app-button__inner">
      <el-icon v-if="loading" class="is-loading"><Loading /></el-icon>
      <slot></slot>
    </span>
  </button>
</template>

<style lang="scss">
.app-button {
  display: inline-block;
  line-height: 1;
  white-space: nowrap;
  cursor: pointer;
  color: #43444d;
  text-align: center;
  box-sizing: border-box;
  outline: none;
  margin: 0;
  transition: 0.1s;
  font-weight: 400;
  padding: 11px 20px;
  font-size: 16px;
  border-radius: 4px;
  background: rgba(26, 56, 96, 0.04);
  border: 1px solid rgba(26, 56, 96, 0.05);
  min-width: 120px;
  &:hover {
    opacity: 0.8;

    .hvr-forward {
      transform: translateX(8px);
    }
  }
  &__inner {
    display: flex;
    align-items: center;
    justify-content: center;
    .svg-icon:first-child {
      margin-right: 5px;
    }
    .svg-icon:last-child {
      margin-left: 5px;
    }
  }
  &.is-round {
    border-radius: 50px;
  }
  &.is-block {
    width: 100%;
  }
  &.is-loading {
    position: relative;
    pointer-events: none;
    &::before {
      z-index: 1;
      pointer-events: none;
      content: '';
      position: absolute;
      left: -1px;
      top: -1px;
      right: -1px;
      bottom: -1px;
      border-radius: inherit;
      background-color: rgba(255, 255, 255, 0.3);
    }

    .el-icon.is-loading {
      animation: rotating 2s linear infinite;
      margin-right: 6px;
    }
  }
  &--primary {
    color: #721d0f;
    background: #fdcb6e;
  }
  &--small {
    min-width: 100px;
    font-size: 14px;
    border-radius: 4px;
    padding: 8px 18px;
  }
  &--large {
    min-width: 158px;
    font-size: 18px;
    border-radius: 8px;
    padding: 14px 22px;
  }
  &--disabled {
    cursor: not-allowed !important;
    opacity: 0.6 !important;
    &:hover {
      cursor: not-allowed !important;
      opacity: 0.6 !important;
    }
  }
}

@media screen and (max-width: 768px) {
  .app-button {
    padding: 6px 10px;
    font-size: 14px;
    min-width: 60px;

    &--small {
      min-width: 60px;
      font-size: 12px;
      border-radius: 4px;
      padding: 6px 10px;
    }

    &--large {
      min-width: 120px;
      font-size: 14px;
      padding: 8px 14px;
    }
  }
}
</style>