<template>
  <div class="cards">
    <div class="card" v-for="(projeto, index) in projetos" :key="index">
      <div class="card-header">
        <h5>{{ projeto.nome }}</h5>
        <div>
          <i class="material-icons icon-button options-button">more_vert</i>
          <div class="card card-options">
            <ul>
              <li v-on:click="renameProject(index)">Renomear</li>
              <li v-on:click="deleteProject(index)">Deletar</li>
            </ul>
          </div>
        </div>
      </div>
      <p>{{ projeto.estacoes }} estações</p>
      <p>{{ projeto.concluidas }} concluidas</p>
      <button class="theme-blue" v-on:click="$router.push('/sites')">Abrir</button>
    </div>
    <button class="fab theme-blue" v-on:click="showCreateProjectWindow = true">
      <i class="material-icons">add</i>
    </button>
    <!-- Create project window: -->
    <div class="blur-div" v-show="showCreateProjectWindow">
      <div class="card creation-window">
        <h5>Novo projeto</h5>
        <input type="text" placeholder="Nome do projeto..." v-model="nome"><br>
        <button class="theme-blue" v-on:click="createProject()">Criar</button>
        <button class="theme-red" v-on:click="showCreateProjectWindow = false">Cancelar</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    data: () => {
      return {
        showCreateProjectWindow: false,
        nome: '',
        
        projetos: [
          { nome: '2,5GHz TDD', estacoes: 0, concluidas: 0 },
          { nome: 'EILD Satélite', estacoes: 27, concluidas: 0 },
          { nome: 'Minas 2018', estacoes: 6, concluidas: 0 },
        ]
      }
    },
    methods: {
      createProject() {
        if (this.nome.replace(/\s/g, "") !== "") {
          this.projetos.push({
            id: this.projetos.length + 1,
            nome: this.nome,
            estacoes: 0,
            concluidas: 0,
          });
          this.showCreateProjectWindow = false
          this.nome = ''
        }
        else {
          alert("Nome iválido")
        }
      },
      deleteProject(index) {
        if (confirm("Deseja excluir esse projeto?")) {
          this.projetos.splice(index, 1)
        }
      },
      renameProject(index) {
        let newName = prompt("Novo nome:")

        if (newName.replace(/\s/g, "") !== "") {
          this.projetos[index].nome = newName
        }
        else {
          alert("Nome iválido")
        }
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .card .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .card-options {
    position: absolute;
    margin-top: -44px;
    margin-left: -59px; 
    display: none; 
  }
  .card-options ul li {
    cursor: pointer;
  }
  .card-options ul li:hover {
    background-color: #F1F1F1
  }
  .options-button:hover + .card-options { 
    display: block;
  }
  .card-options:hover { 
    display: block;
  }
  .fab {
    position: fixed;
    bottom: 15px;
    right: 4%;
  }
</style>
