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
        <textarea id="value" rows="3" v-model.trim="enteredValue"></textarea>
      </div>

      <button
        class="btn primary"
        :disabled="isAddButtonDisable"
        @click.prevent="addBlock"
      >
        Добавить
      </button>
    </form>

    <div class="card card-w70">
      <h3 v-if="blocks.length === 0">
        Добавьте первый блок, чтобы увидеть результат
      </h3>
      <component
        v-for="(block, index) in blocks"
        :key="index"
        :is="block.componentName"
        :payload="block.payload"
      ></component>
    </div>
  </div>
  <app-comments
    commentsUrl="https://jsonplaceholder.typicode.com/comments?_limit=42"
  ></app-comments>
</template>

<script>
import AppSelectType from "./AppSelectType.vue";
import AppTitle from "./AppTitle";
import AppText from "./AppText";
import AppSubtitle from "./AppSubtitle";
import AppAvatar from "./AppAvatar";
import AppComments from "./AppComments.vue";

export default {
  components: {
    AppSelectType,
    AppTitle,
    AppSubtitle,
    AppAvatar,
    AppText,
    AppComments,
  },
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
      blocks: [],
      selectedType: "title",
      enteredValue: "",
    };
  },
  methods: {
    blockTypeChangeHandler(blockType) {
      this.selectedType = blockType;
    },
    addBlock() {
      this.blocks.push({
        componentName: `app-${this.selectedType}`,
        payload: this.enteredValue,
      });
      this.clear();
    },
    clear() {
      this.selectedType = "title";
      this.enteredValue = "";
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
