<template lang="pug">
  div
    nav.navbar.header.has-shadow.is-primary(role='navigation', aria-label='main navigation')
      .navbar-brand
        
        .navbar-burger
          span
            span
              span
    section.main-content
      .container
        nuxt

</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' }
        },
        {
          title: 'Inspire',
          icon: 'lightbulb',
          to: { name: 'inspire' }
        }
      ]
    }
  }
}
</script>
