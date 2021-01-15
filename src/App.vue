<template>
  <div class="container column">
    <form class="card card-w30">
      <app-select-type
        title="Тип блока"
        :items="blockTypeValues"
        :selectedType="selectedType"
        @onTypeChange="blockTypeChangeHandler"
      ></app-select-type>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model="enteredValue"></textarea>
      </div>

      <button class="btn primary" :disabled="isAddButtonDisable">
        Добавить
      </button>
    </form>

    <div class="card card-w70"></div>
  </div>
  <div class="container">
    <p>
      <button class="btn primary">Загрузить комментарии</button>
    </p>
  </div>
</template>

<script>
import AppSelectType from "./AppSelectType.vue";
export default {
  components: { AppSelectType },
  data() {
    return {
      blockTypeValues: [
        {
          value: "title",
          text: "Заголовок",
        },
        {
          value: "subtitle",
          text: "Подзаголовок",
        },
        {
          value: "avatar",
          text: "Аватар",
        },
        {
          value: "text",
          text: "Текст",
        },
      ],
      selectedType: "title",
      enteredValue: "",
    };
  },
  methods: {
    blockTypeChangeHandler(blockType) {
      this.selectedType = blockType;
    },
  },
  computed: {
    isAddButtonDisable() {
      return this.enteredValue.length < 3;
    },
  },
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
