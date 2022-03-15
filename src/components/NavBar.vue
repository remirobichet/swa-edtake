<template>
  <div class="navbar">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <div v-if="!user">
      <div v-for="p in providers" :key="p">
        <span>
          <a :key="p" :href="`/.auth/login/${p}?post_login_redirect_uri=${redirect}`"><h4>{{p}}</h4></a>
        </span>
      </div>
    </div>
    <div v-if="user">
        <p>
            <span>{{user && user.userDetails}} ({{user && user.identityProvider}})</span>
            <span> <a :href="`/.auth/logout?post_logout_redirect_uri=${redirect}`">
                Logout
            </a>
            </span>
        </p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'NavBar',
  props: ['user'],
  data () {
    return {
      providers: ['twitter', 'github', 'aad'],
      redirect: `/`
    }
  }
}
</script>
