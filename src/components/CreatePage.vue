<template>
    <div class="container mb-3">
        <form action="">
            <div class="mb-3">
                <label for="" class="form-label">
                    Page Title
                </label>
                <input 
                    v-model="pageTitle"
                    type="text" 
                    class="form-control"
                />
            </div>
            <div class="mb-3">
                <label for="" class="form-label">
                    Content
                </label>
                <textarea
                v-model="content"
                rows="5" 
                name="" 
                id=""
                class="form-control"
                ></textarea>
            </div>
            <div class="col">
                <div class="mb-3">
                    <label for="" class="form-label">
                        Link Text
                    </label>
                    <input 
                    type="text" 
                    class="form-control"
                    v-model="linkText"
                    />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">
                        Link URL
                    </label>
                    <input 
                    type="text" 
                    v-model="linkUrl"
                    class="form-control"/>
                </div>
                <div class="row mb-3">
                    <div class="form-check">
                        <input type="checkbox" class="form-check-input" v-model="published">
                        <label for="gridCheck1" class="form-check-label">
                            Published
                        </label>
                    </div>
                </div>
            </div>
            <div class="mb-3">
                <button 
                    class="btn btn-primary"
                    :disabled="isFormInvalid"
                    @click.prevent="submitForm()"
                >Create Page</button>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        emits: {
            pageCreated({pageTitle, content, link, published}) {
                if (!pageTitle){
                    return false;
                }
                if (!content){
                    return false
                }
                if (!link || !link.text || !link.url){
                    return false;
                }
                return true;
            }
        },
        computed: {
            isFormInvalid () {
                return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl;
            }
        },
        data() {
            return {
                pageTitle: '',
                content: '',
                linkText: '',
                linkUrl: '',
                published: true
            }
        },
        methods: {
            submitForm() {
                if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
                    alert('Please fill the form')
                    return;
                }

                this.$emit('pageCreated', {
                    pageTitle: this.pageTitle,
                    content: this.content,
                    link: {
                        text: this.linkText,
                        url: this.linkUrl
                    },
                    published: this.published
                });

                this.pageCreated();

                this.pageTitle= '';
                this.content= '';
                this.linkText= '';
                this.linkUrl= '';
                this.published= true;
            }
        },
        watch: {
            pageTitle(newTitle, oldTitle){
                if(this.linkText == oldTitle) {
                    this.linkText = newTitle;
                }
            },
        }
    }
</script>