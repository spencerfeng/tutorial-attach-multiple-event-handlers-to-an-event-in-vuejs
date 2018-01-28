<template>
  <div id="app">
    <img id="logo" src="./assets/logo.png">
    <div class="alert" :class="[alertTypeClass]" v-if="alert.visible">
      {{ alert.message }}
    </div>
    <div class="updated-at">Last updated at {{ updatedAt }}</div>
    <BitcoinPrice @price-request-returned="displayAlertMessage($event); updateTime($event)"/>
  </div>
</template>

<script>
import BitcoinPrice from './components/BitcoinPrice'
import * as moment from 'moment'

export default {
  name: 'App',
  data() {
    return {
      alert: {
        message: '',
        type: '',
        visible: false,
      },
      updatedAt: moment().format('DD/MM/YYYY hh:mm:ss'),
    }
  },
  computed: {
    alertTypeClass() {
      return `alert-${this.alert.type}`;
    }
  },
  components: {
    BitcoinPrice
  },
  methods: {
    displayAlertMessage(data) {
      this.alert.message = data.message;
      this.alert.type = data.success ? 'success' : 'danger';
      this.alert.visible = true;
    },
    updateTime(data) {
      if (data.success) {
        this.updatedAt = moment().format('DD/MM/YYYY hh:mm:ss');
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#logo {
  margin-bottom: 30px;
}
.alert {
  border: 1px solid transparent;
  border-radius: 5px;
  text-align: center;
  padding: 5px 12px;
  margin-bottom: 30px;
}
.alert.alert-success {
  color: #155724;
  background-color: #d4edda;
  border-color: #c3e6cb;
}
.alert.alert-danger {
  color: #721c24;
  background-color: #f8d7da;
  border-color: #f5c6cb;
}
.updated-at {
  font-size: 11px;
  background: #ff9c44;
  color: #ffffff;
  width: 200px;
  text-align: center;
  margin: 10px auto;
  padding: 3px 0;
  border-radius: 3px;
}

</style>
