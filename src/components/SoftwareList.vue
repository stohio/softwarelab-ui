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
  name: 'software-list',
  data () {
    return {
      msg: 'The Software Lab',
      apiUrl:  "http://10.2.0.252:8080",
      servers: [{
        name: "Brick Hack",
        private_ip: "192.168.1.10",
        software: [{"clean_name": "Android Studio", "id" : 1, "name": "android-studio-ide-145.3360264-linux.zip"}, {"clean_name": "JRE 1.8", "id":2 ,"name": "jre-8u121-linux-i586.tar.gz"} , {"clean_name": "Postman", "id":3 ,"name":"Postman-linux-x64-4.9.3.tar.gz"} , {"clean_name": "AuthPy", "id":4 ,"name":"authy-authy-python-f085687.zip"} , {"clean_name": "MonoDevelop", "id":5 ,"name":"monodevelop-6.1.2.44-1.flatpak"} , {"clean_name": "SimpleSMS", "id":6,"name":"simpleSMS-master.zip"} , {"clean_name": "Ngrok x64", "id":7 ,"name":"ngrok-stable-linux-amd64.zip"} , {"clean_name": "Java OCR", "id":8 ,"name":"javaocr-20100605.zip"} , {"clean_name": "JDK 1.8", "id":9 ,"name":"jdk-8u121-linux-i586.tar.gz"} ]
      }]
    }
  },

  mounted () {
    this.fetchServerList()
  },
  methods: {
    fetchServerList () {
      var xhr = new XMLHttpRequest();
        var self = this;
        xhr.open('GET', this.apiUrl + "/server");
        xhr.onload = function() {
          self.servers = JSON.parse(xhr.responseText);
        }
        xhr.send();
    }

  }

}
</script>

<style scoped lang="scss">
#list-container {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  width: 100%;
  max-width: 940px;

  margin: 0 auto;
}

.server {
  width: 100%;
}

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
