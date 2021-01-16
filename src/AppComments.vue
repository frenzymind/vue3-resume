<template>
  <div class="container">
    <p>
      <button class="btn primary" @click="load" v-if="!isCommentsExist">
        Загрузить комментарии
      </button>
    </p>

    <div class="card" v-if="isCommentsExist">
      <h2>Комментарии</h2>
      <ul class="list" v-for="c in comments" :key="c.id">
        <li class="list-item">
          <div>
            <p>
              <strong>{{ c.email }}</strong>
            </p>
            <small>{{ c.body }}</small>
          </div>
        </li>
      </ul>
    </div>
    <div class="container center" v-if="loading">
      <app-spiner></app-spiner>
    </div>
  </div>
</template>

<script>
import AppSpiner from "./AppSpiner.vue";
export default {
  components: { AppSpiner },
  props: {
    commentsUrl: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      comments: [],
      loading: false,
    };
  },
  methods: {
    async load() {
      try {
        this.loading = true;

        const res = await fetch(this.commentsUrl, {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
          },
        });

        const data = await res.json();
        this.comments = data;
      } catch (error) {
      } finally {
        this.loading = false;
      }
    },
  },
  computed: {
    isCommentsExist() {
      return this.comments.length > 0;
    },
  },
};
</script>
<style>
</style>