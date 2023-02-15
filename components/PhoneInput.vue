<template>
  <input type="text" v-bind="$attrs" :value="modelValue" @input="updateValue" maxlength="13" />
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
  props: {
    modelValue: {
      type: String,
    },
  },
  setup(props, { emit }) {
    const updateValue = (event) => {
        let cleaned = event.target.value.replaceAll("(", "").replaceAll(")", "").replaceAll("-", "")
        let formatted = `(${cleaned.substr(0,3)})${cleaned.substr(3,3)}-${cleaned.substr(6,3)}`
        emit("update:modelValue", formatted);
    };
    return { updateValue };
  },
});
</script>
