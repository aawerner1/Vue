<template>
    <div class="painel">
        <h2 class="painel-titulo" @click="visivel = !visivel">{{ titulo }}</h2>

        <transition name="painel-fade">
            <div class="painel-corpo" v-show="visivel">
                <slot>
                </slot><!-- fim painel-corpo -->
            </div>
        </transition>
        
    </div>
</template>

<script>
export default {
    props: ['titulo'],

    data() {
        return {
            visivel: true
        }
    }
}
</script>

<style scoped>

  .painel {
    padding: 0 auto;
    display: inline-block;
    margin: 5px;
    box-shadow: 5px 5px 10px grey;
    width: 200px;
    height: 100%;
    vertical-align: top;
    text-align: center;
  }
  .painel h2 {
    font-size: 14px;
    font-weight: light;
    color: white;
  }

  .painel .painel-titulo {
    text-align: center;
    background: #29335C;
    margin: 0 0 0px 0;
    padding: 10px;
    text-transform: uppercase;
  }

  .painel-fade-enter, 
  .painel-fade-leave {
      opacity: 0;
  }

  .painel-fade-enter-active,
  .painel-fade-leave-active {
      transition: opacity .4s;
  }
</style>
