<template>
  <div class="container column">
    <form class="card card-w30">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3"></textarea>
      </div>

      <button class="btn primary">Добавить</button>
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
export default {};
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
