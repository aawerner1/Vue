<template>
    <nav class="px-o">
      <ul class="nav ">       
          <li class="nav-item" v-for="rota in rotas">
            <router-link :to="rota.path ? rota.path : '/'">{{rota.titulo}}</router-link>
          </li>
      </ul>
    </nav>
</template>

<script>
export default {
   props: {
     rotas: {
      type: Array,
      required: true
     }  
   }
}
</script>

<style >

    nav {
      background-color: #29335C;
      width: 100%;
      margin-bottom: 15px;
    }

    nav li {
      list-style: none;
      margin: 30px 30px;
    }

    nav li a,
    nav li a:hover {
      color: white;
    }
</style>