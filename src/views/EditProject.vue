<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="updateProject">
    <label>Project Title</label>
    <input type="text" v-model="title">

    <label>Project Detail</label>
    <input type="text" v-model="detail">

    <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data() {
        return {
            title: "",
            detail: "",
        }
    },
    methods: {
        updateProject() {
           fetch('http://localhost:3000/projects/' + this.id, {
            method: 'PATCH',
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                title: this.title,
                detail: this.detail,
            })
           })
           .then(() => {
            this.$router.push("/")
           })
           .catch((err) => {
            console.log(err.message());
           });
        }
    },
    mounted() {
        fetch('http://localhost:3000/projects/' + this.id)
        .then((res) => {
            return res.json();
        })
        .then((data) => {
            this.title = data.title;
            this.detail = data.detail;
        })
        .catch((err) => {
            console.log(err.message());
        });
    }
}
</script>

<style>

</style>