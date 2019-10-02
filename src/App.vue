<template>
  <v-app>
    <v-navigation-drawer permanent app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">Application</v-list-item-title>
          <v-list-item-subtitle>subtext</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-content>
      <v-container fluid>
        <v-card v-for="user in users" :key="user.id" style="margin:24px;">
          <v-card-title>User: {{user.name}}</v-card-title>
          <v-card-text>
            id: {{user.id}}
            <br />
            phone: {{user.phone}}
          </v-card-text>
        </v-card>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: "App",
  async mounted() {
    this.loadUsers();
  },
  data: () => ({
    users: [],
    items: [
      { title: "Dashboard", icon: "mdi-view-dashboard" },
      { title: "Photos", icon: "mdi-image" },
      { title: "About", icon: "mdi-help-box" }
    ]
  }),
  methods: {
    loadUsers() {
      fetch("https://jsonplaceholder.typicode.com/users")
        .then(stream => stream.json())
        .then(data => (this.users = data))
        .catch(error => console.error(error));
    }
  }
};
</script>
