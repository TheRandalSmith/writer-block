<template>
    <div>
        <input :value="lastLetter" @keydown="handleInput" readonly/>
        <br />
    </div>
</template>

<script>
    export default {
        data() {
            return {
                lastLetter: ''
            }
        },
        mounted() {
            document.querySelector('input').focus();
        },
        methods: {
            handleInput(e) {
                const letter = e.key;
                if (letter.length === 1) {
                    this.lastLetter = letter;
                } else if (letter.toLowerCase() === 'enter') {
                    this.lastLetter = '\n';
                }
            }
        },
        watch: {
            lastLetter() {
                this.$emit("newInput", this.lastLetter);
            }
        }
    }
</script>

<style scoped>

</style>
