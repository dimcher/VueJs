<template>
<div>
    <table>
        <tr>
            <th v-for="(value, index) in keys" :key="`thead-${index}`">{{head[value]}}</th>
        </tr>
        <tr v-for="(rv, ri) in options" :key="`row-${ri}`">
            <td v-for="(cv, vi) in keys" :key="`value-${vi}`">{{rv[cv]}}</td>
            <OptionDelete :optionId="rv['rooftopGoogleOptionId']" :googleId="googleId" @refreshMe="refreshMe()" />
        </tr>
    </table>
</div>
</template>

<script>
import axios from 'axios';
import OptionDelete from './OptionDelete'
export default {
    name: 'Table',
    components: {
        OptionDelete
    },
    props: {
        account: {
            type: String
        },
        googleId: {
            style: String
        }
    },
    data: () => {
        return {
            keys: ["platformName", "optionName", "optionValue", "dotDigitalId"],
            head: {
                "platformName": "Platform Name", 
                "optionName": "Option Name", 
                "optionValue": "Option Value", 
                "dotDigitalId" : "Digital ID"
            },
            errors: [],
            options: []
        }
    },
    watch: {
        account: function() {
            this.getOptions()
        }
    },
    created: function() {
        this.getOptions()
    },
    methods: {
        refreshMe() {
            this.getOptions()
        },
        getOptions() {
            let that = this;
            console.log("here");
            axios
                .get('https://services.metricsamsi.com/v1.0/dealers/Options/'+ that.account +'?apiKey='+ that.googleId)
                .then(function (response) {
                    that.options = response.data.data;
                })
                .catch(e => {
                    that.errors.push(e);
                });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
</style>
