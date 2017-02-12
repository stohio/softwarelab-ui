<template>

  <div id="list-container">
    <ul 
    class="server-list">
      <li class="server">
        <div class="flex-container" v-bind:class="{hidden: expandList === false}">
          <h3>Available Software {{ searchString }}</h3>
          <input v-model="searchString" type="text" placeholder="Search..." class="big-input"><span class="big-input-line"></span>
        </div>
        <ul class="software-list" v-bind:class="{hidden: expandList === false}">
          <div v-for="software in bundleFilter(searchFilter(server.software))" v-on:click="downloadFile(software)">
            <li class="software-card">
              <img src=""/>
              <h4>{{ software.clean_name }}</h4>
              <p></p>
            </li>
          </div>
        </ul>
        <div class="server-info">
          <h2>{{ server.name }} Server</h2>
          <p>{{ server.ip }}</p>
        </div>
      </li>
    </ul>
    <div class="bundle-card see-all"
      v-on:click="expandListItems"
      v-bind:class="{hidden: expandList}">
        <div class="block"></div>
        <svg viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" fill="#000"><g><path d="M 23.706,15.312L 17.788,8.622c-0.392-0.392-1.030-0.392-1.422,0s-0.392,1.030,0,1.422l 5.3,5.992l-5.3,5.992 c-0.392,0.392-0.392,1.030,0,1.422s 1.030,0.392, 1.422,0l 5.918-6.69c 0.2-0.2, 0.296-0.462, 0.292-0.724 C 24,15.774, 23.906,15.512, 23.706,15.312zM 9.192,23.452c 0.392,0.392, 1.030,0.392, 1.422,0l 5.918-6.69c 0.2-0.2, 0.296-0.462, 0.292-0.724 c 0.004-0.262-0.092-0.526-0.292-0.724L 10.616,8.622c-0.392-0.392-1.030-0.392-1.422,0s-0.392,1.030,0,1.422l 5.3,5.992l-5.3,5.992 C 8.8,22.422, 8.8,23.060, 9.192,23.452z"></path></g></svg>
        <h2>See All Software</h2>
    </div>

  </div>
</template>

<script>
export default {
  name: 'software-list',
  data () {
    return {
      apiUrl:  "http://40.71.25.155:8080",
      searchString: '',
      expandList: false,
      server: {
        name: "Brick Hack",
        private_ip: "",
        software: [{"clean_name": "Android Studio", "id" : 1, "name": "android-studio-ide-145.3360264-linux.zip"}, {"clean_name": "JRE 1.8", "id":2 ,"name": "jre-8u121-linux-i586.tar.gz"} , {"clean_name": "Postman", "id":3 ,"name":"Postman-linux-x64-4.9.3.tar.gz"} , {"clean_name": "AuthPy", "id":4 ,"name":"authy-authy-python-f085687.zip"} , {"clean_name": "MonoDevelop", "id":5 ,"name":"monodevelop-6.1.2.44-1.flatpak"} , {"clean_name": "SimpleSMS", "id":6,"name":"simpleSMS-master.zip"} , {"clean_name": "Ngrok x64", "id":7 ,"name":"ngrok-stable-linux-amd64.zip"} , {"clean_name": "Java OCR", "id":8 ,"name":"javaocr-20100605.zip"} , {"clean_name": "JDK 1.8", "id":9 ,"name":"jdk-8u121-linux-i586.tar.gz"}, {"clean_name": "Android Bundle", "id":10 ,"name":"android_bundle.zip"}]
      },
      bundles: {
          "mobile": [1, 9, 10],
          "java": [2, 8, 9],
          "games": [5],
          "os": [3, 4, 7]
        }
    }
  },

  props: ['openTab'],


  mounted () {

  },
  methods: {
    fetchServerList (callback) {
      var xhr = new XMLHttpRequest();
        var self = this;
        xhr.open('GET', this.apiUrl + "/get_ip");
        xhr.onload = function() {
          self.server.private_ip = xhr.responseText;
          console.log("responseText",xhr.responseText)
          console.log("private_ip",self.server.private_ip)
          callback();
        }
        xhr.send();
    },

    fetchAppList () {
      var xhr = new XMLHttpRequest();
        var self = this;
        xhr.open('GET', this.apiUrl + "/apps");
        xhr.onload = function() {
          self.server.software = JSON.parse(xhr.responseText);
        }
        xhr.send();
    },

    searchFilter(software) {
      var self = this;
      return software.filter(function (software) {

        if (self.searchString === '') {
          console.log("empty");
          return software;
        }
        
        var searchParams = self.searchString.split(' ');

        for (var i = 0; i < searchParams.length; i++) {
          console.log(searchParams[i], software);
          if (software.clean_name.toLowerCase().includes(searchParams[i].toLowerCase()) ) {
            return software;
          } else if ( software.name.toLowerCase().includes(searchParams[i].toLowerCase()) ) {
            return software;
          } else {
            
          }
        }

        return 0;
      })
    },

    bundleFilter(software) {
      var self = this;

      return software.filter(function (software) {

        if (self.openTab != '') {
          console.log(self.bundles[self.openTab], software.id);
        
          for (var i = 0; i < self.bundles[self.openTab].length; i ++) {
            if ( self.bundles[self.openTab][i] === software.id ) {
              return software;
            }
          }
        } else {
          return software;
        }

      })
    }, 

    downloadFile(software) {
      console.log("download", software);
      var self = this;
      var mySoft = software;
      this.fetchServerList(
          function() {

            console.log("private self", self, "private this", this);
            var xhr = new XMLHttpRequest();
              
            xhr.open('GET', "http://"+ self.server.private_ip + ":8080/application?id=" + mySoft.id);
            xhr.onload = function() {
              console.log(JSON.parse(xhr.responseText));
            }
            xhr.send();
          }
      );
    },

    expandListItems: function() {
        this.expandList = true;
        this.$emit('changeBundle', '');
    },

    dontShowAll: function() {
      this.expandList = false;
    }


  }

}
</script>

<style scoped lang="scss">
#list-container {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ddd5bf;
  margin-top: 60px;

  width: 100%;
  max-width: 940px;

  margin: 0 auto;
}

.hidden {
  max-height: 0px;
  overflow: hidden;
  opacity: 0;
}

.server {
  width: 100%;
}

.server-info {
  position: fixed;
  bottom: 0;
  right: -20px;
  opacity: 0.5;
  transform: scale(0.6);
  text-align: right;
}

h3 {
  margin-bottom: 20px;
  text-align: left;
  display: inline-block;
}

.flex-container {
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

.software-card {
  display: block;
  width: 100%;
  background-color: rgba(10, 13, 16, 0.8);
  color: #ddd5bf;

  text-align: left;

  padding: 20px 40px;
  margin-bottom: 20px;

  cursor: pointer;

  border-radius: 5px;
  box-shadow: 0 1px 4px 0 rgba(0,0,0,0.16);

  transition: 0.3s box-shadow ease;

  &:hover {
    box-shadow: 0 3px 6px 0 rgba(0,0,0,0.23);
  }
}
</style>
