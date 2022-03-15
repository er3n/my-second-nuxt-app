<template>
  <div class="admin-post-page">
    <section class="update-form">
      <AdminPostForm :post="loadedPost" @submit="onSubmitted" />
    </section>
  </div>
</template>

<script>
import axios from "axios";
import AdminPostForm from "@/components/Admin/AdminPostForm";

export default {
  layout: "admin",
  middleware: ['check-auth', 'auth'],
  components: {
    AdminPostForm,
  },
  asyncData(context) {
    return axios
      .get(
        "https://nuxt-blog-a029a-default-rtdb.firebaseio.com/posts/" +
          context.params.postId +
          ".json"
      )
      .then((res) => {
        return {
          loadedPost: { ...res.data, id: context.params.postId },
        };
      })
      .catch((e) => context.error(e));
  },
  methods: {
    onSubmitted(editedPost) {
      this.$store
        .dispatch("editPost", editedPost)
        .then((res) => {
          this.$router.push("/admin");
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style scoped>
.update-form {
  width: 90%;
  margin: 20px auto;
}
@media (min-width: 768px) {
  .update-form {
    width: 500px;
  }
}
</style>