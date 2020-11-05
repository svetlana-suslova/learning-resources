<template>
    <base-card>
        <base-button @click="setSelectedTab('resources-list')" :mode="listResButtonMode">Resorces List</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
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
            resources: this.storedResources,
            addResource: this.addResource,
            removeResource: this.removeResource
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
        },
        addResource(title, desc, link) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: desc,
                link: link
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'resources-list';
        },
        removeResource(resId) {
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        }
    }
}
</script>