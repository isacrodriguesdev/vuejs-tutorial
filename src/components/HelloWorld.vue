<template>
  <h1>{{ fullName }}</h1>

  <h1 v-if="isLoading">Loading...</h1>

  <MyUser v-for="(user, index) in users" :key="index" :user="user" />

  <input type="text" v-model="name" />

  <button @click="(e) => onClick(e)">Click</button>
  <button @click="() => changeName('Alice')">Change Name</button>
</template>

<script>
import MyUser from './MyUser.vue'

function onClick(event) {
  console.log(event)
}

// simular uma chamada para uma API
function fetchUsers() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve([
        { name: 'Bob' },
        { name: 'Aline' },
        { name: 'Jane' }
      ])
    }, 2000)
  })
}

export default {
  name: 'HelloWorld',
  components: {
    MyUser
  },
  props: {
    msg: String
  },
  data() {
    return {
      isLoading: true,
      name: '',
      firstName: 'John',
      lastName: 'Doe',
      users: [],
    }
  },
  async mounted() {
    this.users = await fetchUsers();
    this.isLoading = false;
  },
  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`;
    },
  },
  watch: {
    firstName(newValue, oldValue) {
      console.log(newValue, oldValue);
    }
  },
  methods: {
    changeName(name) {
      this.firstName = name;
    },
    onClick,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>