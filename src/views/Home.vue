<template>
<div>
  <div v-if="loading">
    <page-loading/>
  </div>
  <transition>
    <div v-if="api" class="conteudo">
      <div>
        <h1> Sobre a {{api.titulo}} </h1>
        <p>{{api.descricao}}</p>
        <router-link class="btn-cursos" tag="button" to="/cursos">Cursos</router-link>
        <div>
          <h2>Avaliações</h2>
          <ul>
            <li v-for="avaliacao in api.avaliacoes" :key="avaliacao.nome">
              <p>{{avaliacao.nome}}</p> 
              <p>{{avaliacao.descricao}}</p> 
            </li>
          </ul>
        </div>
     </div>
     <img src="../assets/learn.png" alt="Aprenda Web Design">
   </div>
  </transition>
</div>
</template>

<script>
import PageLoading from '../components/PageLoading.vue';
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
            this.api = r.home;
         this.loading = false;
        }, 1500)
      });
    }
  }
};

export default {
  components: { PageLoading },
  name: "home",
  mixins: [fetchData],
  created() {
    this.fetchData();
  }
};
</script>

<style>
.btn-cursos {
  border: none;
  background: #4b8;
  border-radius: 4px;
  color: white;
  cursor: pointer;
  padding: 15px 40px;
  font-size: 1rem;
  margin-bottom: 40px;
  margin-top: 10px;
  box-shadow: 0 4px 2px rgba(0,0,0,.1);
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}

</style>