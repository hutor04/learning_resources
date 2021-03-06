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
    <component :is="selectedTab"></component>
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
    }
  };
</script>

<style scoped>

</style>
