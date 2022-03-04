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
        <li>
          <b>Email: </b>
          {{api.contato.email}}
        </li>
        <li>
          <b>Telefone: </b>
          {{api.contato.telefone}}
        </li>
        <li>
          <b>Endereço: </b>
          {{api.contato.endereco}}
        </li>
      </ul>
    </div>
  </transition>
</div>
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
            this.api = r.contato;
         this.loading = false;
        }, 1500)
      });
    }
  }
 };


export default {
  name: "contato",
  mixins: [fetchData],
  created() {
    this.fetchData();
  }
};
</script>
