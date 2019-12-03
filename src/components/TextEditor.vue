<template>
    <div ref="editor" v-html="value"></div>
</template>

<script>
    import Quill from 'quill';

    export default {
        props: {
            value: {
                type: String,
                default: ''
            }
        },

        data() {
            return {
                editor: null
            };
        },
        mounted() {
            this.editor = new Quill(this.$refs.editor, {
                modules: {
                    toolbar: [
                        [{ header: [1, 2, 3, 4, false] }],
                        ['bold', 'italic', 'underline'],
                        ['save']
                    ]
                },
                theme: 'snow',
                formats: ['bold', 'underline', 'header', 'italic']
            });

            this.editor.root.innerHTML = this.value;

            // We will add the update event here
            this.editor.on('text-change', () => this.update());

            //idk why this doesn't work
            this.editor.focus();
        },
        methods: {
            update() {
                this.$emit('input', this.editor.getText() ? this.editor.root.innerText : '');
            }
        }
    }
</script>

<style scoped>

</style>
