<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >StoredResources</base-button
    >
    <base-button
      :mode="addResButtonMode"
      @click="setSelectedTab('add-resources')"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>
<script>
import StoredResources from './StoredResources.vue';
import AddResources from './AddResources.vue';
export default {
  components: {
    StoredResources,
    AddResources,
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab == 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab == 'add-resources' ? null : 'flat';
    },
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The Official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Learn how to Google',
          description: 'Google will help solve things faster',
          link: 'https://google.org',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResources: this.removeResources,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newRes = {
        id: new Date().toUTCString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(newRes);
      this.selectedTab = 'stored-resources';
    },
    removeResources(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>
