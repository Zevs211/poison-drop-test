<template>
  <div class="input">
    <div class="input__label">{{ label }}</div>
    <div
      class="input__container"
    >
      <input
        type="text"
        :placeholder="placeholder"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "VInput",
  props: ['modelValue', 'label', 'placeholder', 'disabled', 'required'],
  emits: ['update:modelValue'],
};
</script>

<style lang="scss" scoped>
.input {
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 24px;
  color: #000000;

  &__label {
    margin-bottom: 8px;
  }
  &__container {
    display: flex;
    align-items: center;
    height: 40px;
    padding: 0 10px;
    border: 1px solid #dfe3e6;
    border-radius: 3px;
    background-color: white;
    transition: border-color 0.25s;

    &:not(.disabled):hover {
      border-color: #000000;
    }

    input {
      width: 100%;
      outline: none;

      font-style: inherit;
      font-weight: inherit;
      font-size: inherit;
      line-height: inherit;
      color: inherit;
    }
  }
}
</style>