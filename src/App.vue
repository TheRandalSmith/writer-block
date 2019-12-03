<template>
    <div id="app">
        <div v-if="wordGoal <= 0 ">
            <label>
                Please Enter a Word Goal:
                <input v-model="newWordGoal"
                       placeholder="Enter a number"
                       @keydown.enter="wordGoal = newWordGoal"
                       type="number"/>
                <button @click="wordGoal = newWordGoal">Submit</button>
            </label>
        </div>
        <div v-else>
            <div v-if="wordsLeft > 0">
                <AppInput @newInput="sentence+=$event"/>
                <p>Words Left: {{wordsLeft}}</p>
            </div>
            <TextEditor v-else
                        :value="sentence"
                        @input="handleTextEditorUpdate"/>
        </div>
    </div>
</template>

<script>
    import AppInput from "./components/AppInput";
    import TextEditor from "./components/TextEditor";

    export default {
        name: 'app',
        components: {
            AppInput,
            TextEditor,
        },
        data() {
            return {
                sentence: "",
                wordGoal: 0,
                newWordGoal: null,
            };
        },
        methods: {
            handleTextEditorUpdate(e) {
                // eslint-disable-next-line no-console
                console.log(e);
                
            }
        },
        computed: {
          wordCount() {
            return this.sentence.split(" ").length;
          },
            wordsLeft() {
                return this.wordGoal - this.sentence.split(" ").length + 1;
            }
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
