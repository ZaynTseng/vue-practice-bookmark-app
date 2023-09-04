<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')"
                 :mode="storeBtnMode">Stored Resources
    </base-button>
    <base-button @click="setSelectedTab('add-resource')"
                 :mode="addBtnMode">Add Resource
    </base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import AddResource from "@/components/learning-resources/AddResource.vue";
import StoredResources from "@/components/learning-resources/StoredResources.vue";

export default {
  components: {
    StoredResources,
    AddResource
  },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "0001",
          title: "Official Guide",
          description: "The official guide to learn Vue.js",
          link: "https://vuejs.org"
        },
        {
          id: "0002",
          title: "Google",
          description: "Google will be a good starting point",
          link: "https://google.com"
        }
      ]
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      add: this.addNewResource,
      remove: this.removeResource
    };
  },
  computed: {
    storeBtnMode() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    addBtnMode() {
      return this.selectedTab === "add-resource" ? null : "flat";
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addNewResource(title, desc, link) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: desc,
        link: link
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = "stored-resources";
    },
    removeResource(id) {
      const resIndex = this.storedResources.findIndex(res => res.id === id);
      this.storedResources.splice(resIndex, 1); // manipulates the original array
    }
  }
};
</script>
