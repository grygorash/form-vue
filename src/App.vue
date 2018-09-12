<template>
  <div id="app" class="app">
    <Form />
  </div>
</template>

<script>
  import Form from './components/Form';

  export default {
    name: 'App',
    components: {
      Form
    }
  };
</script>

<style lang="sass">
  body
    margin: 0
    font-family: 'Roboto', sans-serif
    .app
      width: 400px
      margin: 50px auto 0
      .main-btn
        width: 220px
        height: 40px
        background: #42bef5
        border: none
        border-radius: 20px
        color: white
        text-transform: uppercase
        cursor: pointer
        margin: 20px auto 0
        transition: all .3s
        &:hover
          background: #3250aa
        &.disabled
          background-color: #eee
          cursor: default
          pointer-events: none
      input, button
        outline: none
      input
        color: #3250aa
        &:focus
          border-color: #3250aa
</style>
