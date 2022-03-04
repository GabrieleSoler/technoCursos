<template>
<div>
  <div v-if="loading">
    <page-loading/>
  </div>
  <transition>
    <div v-if="api">
      <h1>{{api.titulo}}</h1>
      <p>{{api.descricao}}</p>
      <ul>
        <li v-for="curso in api.cursos" :key="curso.id">
          <h2>
            <router-link :to="{name: 'curso', params: {curso: curso.id}}">{{curso.nome}} - {{curso.totalAulas}} aulas | {{curso.horas}} horas</router-link>
            </h2>
          <p>{{curso.descricao}}</p>
        </li>
      </ul>
    </div>
  </transition>
</div>
</template>

<script>
const fetchData =  {
  data() {
    return {
      api: null,
      loading: true
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
            this.api = r.cursos;
         this.loading = false;
        }, 1000)
      });
    }
  }
};

export default {
  name: "cursos",
  mixins: [fetchData],
  created() {
    this.fetchData();
  }
};
</script>