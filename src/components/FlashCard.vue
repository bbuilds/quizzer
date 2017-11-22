<template>
  <div class="ui centered card">
      <div class="content">
          <header class="header">
              {{card.term}}
          </header>
          <div class="decription">
              {{card.definition}}
          </div>
      </div>
  </div>
</template>

<script>

export default {
  props: ['card']
}
</script>

<style>
</style>