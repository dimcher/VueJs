<template>
    <div>
        <div class="sign">Option Editor</div>
        <div>Option: {{option.rooftopGoogleOptionId}}</div>
        <div class="inputs" v-for="(v, i) in keys" :key="`row-${i}`">
            <div class="desc">{{ head[v] }}</div>
            <div class="input"><input type="text" :name="`${v}`" :value="option[v]"></div>
        </div>
        <button @click="procProps">SUBMIT</button>
        <button @click="closeAction">CANCEL</button>
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
            errors: []
        }
    },
    methods: {
        closeAction: function () {
            this.$emit('doAction', {});
        },
        procProps: function () {
            let props = {};
            for(const key of this.keys) {
                props[key] = document.querySelector("input[name="+ key + "]").value;
            }
            let that = this;
            axios
                .patch('https://services.metricsamsi.com/v1.0/dealers/Options/'+ that.option.rooftopGoogleOptionId +'?apiKey='+ that.googleId, props)
                .then(function () {
                    that.closeAction();
                })
                .catch(e => {
                    that.errors.push(e);
                    that.closeAction();
                });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .sign { color: red; }
    input { width: 300px; }
    button { font-weight: bold; }
    .inputs { margin: 10px; }
    .inputs > div.desc { font-weight: bold; }
</style>
