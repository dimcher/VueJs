<template>
    <div>
        <div class="sign">Option Editor</div>
        <div>Option: {{option.rooftopGoogleOptionId}}</div>
        <p v-for="(v, i) in keys" :key="`row-${i}`">
            {{ head[v] }} <input type="text" :name="`${v}`" :value="option[v]">
        </p>
        <button @click="cancelEdit">CANCEL</button>
        <button @click="editProps">SUBMIT</button>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'OptionEdit',
    props: {
        option: {
            type: Object
        },
        keys: {
            type: Array
        },
        head: {
            type: Object
        },
        googleId: {
            style: String
        }
    },
    data: () => {
        return {
        }
    },
    methods: {
        cancelEdit: function () {
            this.$emit('doAction', {});
        },
        editProps: function () {
            let props = {};
            for(const key of this.keys) {
                props[key] = document.querySelector("input[name="+ key + "]").value;
            }
            let that = this;
            axios
                .patch('https://services.metricsamsi.com/v1.0/dealers/Options/'+ that.option.rooftopGoogleOptionId +'?apiKey='+ that.googleId, props)
                .then(function () {
                    console.log("done");
                })
                .catch(e => {
                    that.errors.push(e);
                });
            this.$emit('editedProps', props);
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .sign { color: red; }
    input { width: 300px; }
    button { font-weight: bold; }
</style>
