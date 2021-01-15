<template>
  <div class="form-control">
    <label :for="selectId" v-text="title"></label>
    <select :id="selectId" @change="$emit('onTypeChange', $event.target.value)">
      <option
        v-for="item in items"
        :key="item"
        :value="item.value"
        v-text="item.text"
        :selected="item.value === selectedType"
      ></option>
    </select>
  </div>
</template>

<script>
export default {
  props: ["title", "items", "selectedType"],
  emit: ["onTypeChange"],
  data() {
    return {
      selectId: "type" + Math.random(),
    };
  },
};
</script>
<style>
</style>