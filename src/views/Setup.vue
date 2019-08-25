<template>
  <div class="setup">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <div>
          <input type="text" v-model="setupOptions.username" placeholder="username" />
        </div>
        <div>
          <input type="password" v-model="setupOptions.password" placeholder="password" />
        </div>
        <div>
          <input type="text" v-model="setupOptions.baseUrl" placeholder="baseUrl" />
        </div>
        <div>
          <input type="text" v-model="setupOptions.apiExtension" placeholder="apiExtension" />
        </div>
        <div>
          <input type="text" v-model="setupOptions.jql" placeholder="jql" />
        </div>
        <div>
          <input type="submit" value="Submit" />
        </div>
        <div v-bind:model="status"></div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      setupOptions: {
        username: "",
        password: "",
        baseUrl: "",
        apiExtension: "",
        jql: ""
      },
      status: ""
    };
  },
  created: function() {
    chrome.storage.sync.get({
        username: this.setupOptions.username,
        password: this.setupOptions.password,
        description: this.setupOptions.description,
        baseUrl: this.setupOptions.baseUrl,
        apiExtension: '/rest/api/2',
        jql: 'assignee=currentUser()'
      })
      .then(() => {
        this.status = "Options Saved";
      });
  },
  methods: {
    submit: function() {
      chrome.storage.sync.set({
        username: this.setupOptions.username,
        password: this.setupOptions.password,
        baseUrl: this.setupOptions.baseUrl,
        apiExtension: this.setupOptions.apiExtension,
        jql: this.setupOptions.jql
      });
    }
  }
};
</script>
