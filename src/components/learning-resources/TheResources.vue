<template>
    <base-card>
        <base-button
                @click="setSelectedTab('stored-resources')"
                :mode="storedResButtonMode"
        >Stored Resources
        </base-button>
        <base-button
                @click="setSelectedTab('add-resource')"
                :mode="addResButtonMode"
        >Add Resources</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
  import StoredResources from './StoredResources';
  import AddResource from './AddResource';

  export default {
    name: 'TheResources',
    components: {
      StoredResources,
      AddResource,
    },
    data() {
      return {
        selectedTab: 'stored-resources',
        storedResources: [
          { id: 'official-guide',
            title: 'Official Guide',
            description: 'The official Vue.js documentation',
            link: 'https://vuejs.org'
          },
          { id: 'google',
            title: 'Google',
            description: 'Let me google that for you.',
            link: 'https://google.com'
          },
        ],
      };
    },
    provide() {
      return {
        resources: this.storedResources,
        addResource: this.addResource,
        removeResource: this.removeResource,
      };
    },
    computed: {
      storedResButtonMode() {
        return this.selectedTab === 'stored-resources' ? null : 'flat';
      },
      addResButtonMode() {
        return this.selectedTab == 'add-resources' ? null : 'flat';
      },
    },
    methods: {
      setSelectedTab(tab) {
        this.selectedTab = tab;
      },
      addResource(title, description, link) {
        const newResource = {
          id: new Date().toISOString(),
          title: title,
          description: description,
          link: link,
        };
        this.storedResources.push(newResource);
        this.selectedTab = 'stored-resources';
      },
      removeResource(resId) {
        const resIndex = this.storedResources.findIndex(res => res.id === resId);
        this.storedResources.splice(resIndex, 1);
      },
    }
  };
</script>

<style scoped>

</style>
