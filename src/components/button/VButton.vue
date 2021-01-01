<template>
  <button @click="click" class="mdc-button" :class="klass" ref="root">
    <div v-if="ripple" class="mdc-button__ripple"></div>
    <span v-if="label" class="mdc-button__label">{{ label }}</span>
    <slot />
    <div v-if="touch" class="mdc-button__touch"></div>
  </button>
</template>

<script lang="ts">
import {
  computed,
  defineComponent,
  onBeforeUnmount,
  onMounted,
  ref
} from "vue";
import { MDCRipple } from "@material/ripple";

export default defineComponent({
  name: "VButton",
  props: {
    label: {
      type: String
    },
    outlined: {
      type: Boolean
    },
    raised: {
      type: Boolean
    },
    unelevated: {
      type: Boolean
    },
    touch: {
      type: Boolean,
      default: true
    },
    ripple: {
      type: Boolean,
      default: true
    }
  },
  emits: ["click"],
  setup(props, { emit }) {
    const click = () => {
      emit("click");
    };
    const root = ref();
    const _ripple = ref<MDCRipple>();
    onMounted(() => {
      if (props.ripple) {
        _ripple.value = new MDCRipple(root.value);
      }
    });
    onBeforeUnmount(() => {
      _ripple.value?.destroy();
    });
    const klass = computed(() => {
      return {
        "mdc-button--outlined": props.outlined,
        "mdc-button--raised": props.raised,
        "mdc-button--unelevated": props.unelevated,
        "mdc-button--touch": props.touch
      };
    });
    return {
      click,
      klass,
      root
    };
  }
});
</script>

<style lang="scss">
@import "@material/button/mdc-button";
</style>
