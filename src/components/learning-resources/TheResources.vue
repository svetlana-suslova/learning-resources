<template>
    <base-card>
        <base-button @click="setSelectedTab('resources-list')" :mode="listResButtonMode">Resorces List</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
    <component :is="selectedTab"></component>
</template>

<script>
import ResourcesList from './ResourcesList';
import AddResource from './AddResource';
export default {
    components: {
        ResourcesList,
        AddResource
    },
    data() {
        return {
            selectedTab: 'resources-list',
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to google...',
                    link: 'https://google.com'
                }
            ]
        };
    },
    provide() {
        return {
            resources: this.storedResources
        }
    },
    computed: {
        listResButtonMode() {
            return this.selectedTab === 'resources-list' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        }
    }
}
</script>