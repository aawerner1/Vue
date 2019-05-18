<template>
    <div>
        <h2 class="centralizado">Cadastro</h2>
        <h5 class="centralizado gray">{{ foto.titulo }}</h5>

        <form @submit.prevent="grava()">
            <div class="controle">
                <label for="titulo">Título</label>
                <input id="titulo" autocomplete="off" v-model="foto.titulo">
            </div>

            <div class="controle">
                <label for="url">Url</label>
                <input id="url" autocomplete="off" v-model.lazy="foto.url">
                <imagem-responsiva :url="foto.url" :titulo="foto.titulo"/>
            </div>

            <div class="controle">
                <label for="descricao">Descrição</label>
                <textarea id="descricao" autocomplete="off" v-model="foto.descricao"></textarea>
            </div>

            <div class="centralizado">
                <meu-button rotulo="GRAVAR" tipo="submit"/>
                <router-link to="/">
                
                <meu-button rotulo="VOLTAR" tipo="button"/>
                </router-link>
            </div>

        </form>
    </div>
</template>

<script>

import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue'
import Button from '../shared/button/Button.vue';
import Foto from '../../domain/foto/Foto.js'

export default {
    components: {
        'imagem-responsiva' : ImagemResponsiva,
        'meu-button': Button
    },

    data() {
        return {
            foto: new Foto()
        } 
    },
    methods: {
        grava() {
            this.$http
                .post('v1/fotos', this.foto)
                .then(() => this.foto = new Foto(), err => console.log(err))
        }
    },

  
}
</script>

<style scoped>

  .centralizado {
    text-align: center;
  }
  .controle {
    font-size: 1.2em;
    margin-bottom: 20px;

  }
  .controle label {
    display: block;
  }

 .controle label + input, .controle textarea {
    width: 100%;
    font-size: inherit;
    border-radius: 5px;
    border: 1px solid #ccc;

  }

  .centralizado {
    text-align: center;
  }

  .gray {
      color: #ccc;
  }

</style>