<template>
  <button
    @click="click()"
    :data-disabled="!!disabled"
    :data-loading="!!loading"
  >
    <NuxtIcon v-if="loading" name="animated/loading" filled />
    <span v-else v-text="text" />
  </button>
</template>

<script setup lang=ts>
const props = defineProps<{
  text: string
  loading?: boolean
  disabled?: boolean
  triggerWhileDisabled?: boolean
}>()

const emit = defineEmits([ 'bclick' ])

function click() {
  if (!props.disabled || props.triggerWhileDisabled)
    emit('bclick')
}
</script>

<style scoped lang=scss>
button {
  background-color: $color-green;
  text-align: center;
  width: 100%;
  height: $menu-item-outer-height;
  border-radius: 999pt;
  border: none;
  outline: none;
  padding: $menu-item-padding;
  transition: background-color .1s ease;
  user-select: none;
  cursor: pointer;

  & > * {
    color: #ffffff;
    font-family: $font-major;
    font-size: 10pt;
  }

  .nuxt-icon {
    font-size: 14pt;
  }

  &[data-disabled=true] {
    background-color: $bg-darker;
    cursor: not-allowed;
  }

  &[data-loading=true] {
    opacity: .6;
    cursor: not-allowed;
  }

  [view-mode=desktop] &:hover:not(:disabled) {
    background-color: $color-greenH;
  }
}
</style>
