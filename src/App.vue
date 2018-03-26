<template>
  <div id='app'>
    <Header/>
    <Library/>
  </div>
</template>

<script>
import Header from './components/Header';
import Library from './components/Library';

export default {
  name: 'App',
  components: {
    Header,
    Library,
  },
};
</script>


