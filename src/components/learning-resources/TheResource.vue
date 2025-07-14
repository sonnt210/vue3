<template>
    <base-card>
        <base-button 
        @click="setSelectedTab('stored-resource')" 
        :mode="storedResButtonMode">
        Stored Resources
        </base-button>
        <base-button 
        @click="setSelectedTab('add-resource')"
        :mode="addResButtonMode">
        Add Resource
    </base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>  
    </keep-alive>
</template>

<script>
import StoredResource from './StoredResource.vue';
import AddResource from './AddResource.vue';
export default {
    components: {
        StoredResource,
        AddResource
    },
    data() {
        return { 
            selectedTab:'stored-resource',
            storedResource: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to Google...',
                    link: 'https://google.com'
                },                
            ]
        };
    },
    provide() {
        return {
            resources: this.storedResource,
            addResource: this.addResource
        };
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resource' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, desc, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: desc,
                link: url
            };

            this.storedResource.unshift(newResource);
            this.selectedTab = 'stored-resource';
        }
    }
}
</script>