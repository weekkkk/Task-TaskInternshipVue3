<template>
  <select 
  v-model="modelValue" 
  @change="changeOptions" 
  class="select"
  >
      <option hidden selected disabled value="">Sort from</option>
      <option 
      v-for="option in options" 
      :key="option.value" 
      :value="option.value"
      >
      {{option.name}}
      </option>
  </select>
</template>

<script>
export default {
    name: 'my-select',
    props: {
        modelValue: {
            type: String
        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeOptions(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style>
.select {
    font-weight: bold;
    color: #2d2c30;
    background-color: #e5eaee;
    border: 1px solid #2d2c30;
    border-radius: 10px;
    padding: 15px;
}
</style>