<template>
    <Navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index) => activePage = index"
    ></Navbar>
    <PageViewer
    :page="pages[activePage]"
    ></PageViewer>
</template>

<script>
import Navbar from './components/Navbar.vue'
import PageViewer from './components/PageViewer.vue'
import '../node_modules/bootstrap/dist/css/bootstrap.css';

export default{
    components: {
        Navbar,
        PageViewer
    },
    created() {
        this.getPages()
    },
    data(){
        return {
            activePage: 0,
            pages: this.getPages
        }
    },
    methods: {
        async getPages() {
            let res = await fetch('pages.json')
            let data = await res.json()
            this.pages = data;
        }
    }
}
</script>