<template>

  <div id="list-container">
    <h1>{{ msg }}</h1>
    <ul class="server-list">
      <li v-for="server in servers" class="server">
        <h2>{{ server.name }} Server</h2>
        <p>{{ server.private_ip }}</p>
        <input type="text" placeholder="Search..." class="big-text">
        <h3>Available Software</h3>
        <ul class="software-list">
          <a href="#" v-for="software in server.software">
            <li class="software-card">
              <img src=""/>
              <h1>{{ software.clean_name }}</h1>
              <p></p>
            </li>
          </a>
        </ul>
      </li>
    </ul>
    

  </div>
</template>

<script>
export default {
  name: 'bundle-list',
  data () {
    return {
      msg: 'The Software Lab'
    }
  },

  mounted () {

  },
  methods: {

  }

}
</script>

<style scoped lang="scss">

// a {
//   color: #42b983;
// }

.software-card {
  display: block;
  width: 100%;
  background-color: rgba(10, 13, 16, 0.8);
  color: #ddd5bf;

  text-align: left;

  padding: 20px 40px;
  margin-bottom: 5px;

  border-radius: 5px;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,0.16);

  transition: 0.3s box-shadow ease;

  &:hover {
    box-shadow: 0 3px 6px 0 rgba(0,0,0,0.23);
  }
}
</style>
