<template>
  <p v-if="api">{{api}}</p>
</template>

<script>
const fetchData = {
 data() {
    return {
      loading: true,
      api: null
    }
  },
  methods: {
    fetchData() {
      this.loading = true;
      this.api = null;
      fetch(`http://localhost:5500/aa.json`)
      .then(r => r.json())
      .then(r => {
      setTimeout(() => {
            this.api = r.curso;
         this.loading = false;
        }, 1500)
      });
    }
  }
 };
export default {
  name: "curso",
  props: ["curso"],
  mixins: [fetchData],
   created() {
    this.fetchData(`/curso/${this.curso}`);
  }
}

</script>

<style>

</style>