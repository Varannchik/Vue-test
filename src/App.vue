<template>
  <div id="app">
    <header>
      <img alt="Vue logo" src="./assets/logo.png">
    </header>     
    <main><router-view/></main>
  </div>
</template>

<script>
export default {
  name: 'App',
  metaInfo() {
    return {
      title: 'Live search',
      meta: [      
        { name: 'description', content: 'Pages description can be here' },      
      ]
    }
  }
}
</script> 
