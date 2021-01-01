<template>
  <VButton label="Text" />
  <VButton label="Outlined" outlined />
  <VButton label="Raised" raised />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { VButton } from "@/components/button/";

export default defineComponent({
  components: {
    VButton
  }
});
</script>
