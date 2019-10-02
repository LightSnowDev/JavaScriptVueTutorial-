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
      <v-dialog v-model="dialog" width="500">
        <template v-slot:activator="{ on }"></template>

        <v-card>
          <v-card-title>User Daten</v-card-title>

          <v-card-text>
            <pre>{{dialogUser}}</pre>
          </v-card-text>

          <v-card-actions>
            <div class="flex-grow-1"></div>
            <v-btn color="primary" text @click="dialog = false">I accept</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-container fluid>
        <v-card v-for="(user,i) in users" :key="user.id" style="margin:24px;">
          <v-card-title>User: {{user.name}}</v-card-title>
          <v-card-text>
            id: {{user.id}}
            <br />
            phone: {{user.phone}}
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn
              color="red lighten-2"
              dark
              @click="dialog = true; dialogUser = user;"
            >Click Me To Show Everything</v-btn>
            <v-btn color="green" @click="users.splice(i,1)">User löschen</v-btn>
          </v-card-actions>
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
    dialog: false,
    dialogUser: {},
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
