<template>
    <button @click="disparaAcao()" :class="estiloDoBotao" :type="tipo">{{ rotulo }}</button>
</template>

<script>
export default {

    props: {
        tipo: {
            required: true,
            type: String
        },
        rotulo: {
            required: true,
            type: String
        },
        confirmacao: Boolean,
        estilo: String
    },
    methods: {
        disparaAcao() {
            if(this.confirmacao) {

               if(confirm('Confirma operacao?')) {
                    this.$emit('botaoAtivado');
               }
               return;
            }
           this.$emit('botaoAtivado');      
        }
    },
    computed: {
        estiloDoBotao() {
            if(this.estilo == 'padrao' || !this.estilo) return 'btn btn-primary';
            if(this.estilo == 'danger') return 'btn btn-danger';
        }
    }
}
</script>

<style lang="">
    .btn {
        display: inline-block;
        border-radius: 3px;
        margin: 10px 0px;
        font-size: 14px;
    }
</style>