
<template>
    <nav 
        :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
    >
        <div class="container-fluid">
            <a href="#" class="navbar-brand">My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <navbar-link
                :page="page"
                :index="index"
                :isActive="activePage == index"
                @activated="$emit('activated')"
                v-for="(page, index) in publishedPages" class="nav-item" :key="index"
                ></navbar-link>
            </ul>
            <form action="" class="d-flex">
                <button 
                @click.prevent="changeTheme()"
                class="btn btn-primary">Toggle</button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';

export default {
    components: {
        NavbarLink
    },
    created() {
        this.getThemeSetting();
    },
    computed: {
        publishedPages() {
            return this.pages.filter(p => p.published);
        }
    },
    props:['pages', 'activePage' ],
    data() {
            return {
                theme: 'light',
            }
        },
        methods: {
            changeTheme() {
                let theme = 'light';

                if(this.theme == 'light'){
                    theme = 'dark';
                }
                this.theme = theme;
                this.storeThemeSetting();
            },
            storeThemeSetting() {
                localStorage.setItem('theme', this.theme);
            },
            getThemeSetting() {
                let theme = localStorage.getItem('theme');
                console.log(theme)
    
                if (theme) {
                    this.theme = theme;
                }
            }
        }
}
</script>
