<template>
  <div>

    <h1 class="titulo">{{ titulo }}</h1>

    <p v-show="mensagem" class="centralizado">{{ mensagem }}</p>


    <input type="search" class="filtro" placeholder="Filtre a imagem desejada" @input="filtro = $event.target.value">

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto in fotosComFiltro">

      <meu-painel :titulo="foto.titulo">
        <imagem-responsiva v-meu-transform:scale.animate="1.1" :url="foto.url" :titulo="foto.titulo"></imagem-responsiva>

        <meu-button 
            tipo="button" 
            rotulo="Adicionar" 
            :confirmacao="false">
        </meu-button>
        <meu-button 
            tipo="button" 
            rotulo="Remover" 
            :confirmacao="true"
            @botaoAtivado="remove(foto)"
            estilo="danger">
        </meu-button>
      </meu-painel>
      

      </li>
    </ul>

  </div>
</template>

<script>
import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
import Button from '../shared/button/Button.vue'

export default {
  components: {
    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva,
    'meu-button': Button
  },

  data() {
    return {
      titulo: 'AppPic',
      fotos: [],
      filtro: '',
      mensagem: '',
    }
  },
  created() {
    let promise = this.$http.get('v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, er => console.log(err));
  },
  methods: {
      remove(foto) {
        this.$http
          .delete(`v1/fotos/${foto._id}`)
          
          .then(() => {
            let indice = this.fotos.indexOf(foto)
            this.fotos.splice(indice,1)
            this.mensagem = "Foto removida com sucesso"

            }, 
            
            err => {
            console.log(err),
            this.mensagem = "Erro ao remover"
          });
      }
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  } 
}
</script>

<style>

  h1 {
    color: #29335C;
    margin-bottom:30px;
  }

  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    border: 1px solid #ccc;
    border-radius: 10px;
   -webkit-appearance: none;
    padding: 10px;
    width: 100%;
  }
</style>
