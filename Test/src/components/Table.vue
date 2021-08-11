<template>
<div>
    <table>
        <tr>
            <th v-for="(value, index) in keys" :key="`thead-${index}`">{{head[value]}}</th>
        </tr>
        <tbody :key="JSON.stringify(options)">
            <tr v-for="(rv, ri) in options" :key="`row-${ri}`">
                <td v-for="(cv, vi) in keys" :key="`value-${vi}`">{{rv[cv]}}</td>
                <OptionEdit :optionId="rv['rooftopGoogleOptionId']" :googleId="googleId" @refreshList="refreshMe" />
                <OptionDelete :optionId="rv['rooftopGoogleOptionId']" :googleId="googleId" @refreshList="refreshMe" />
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>
import axios from 'axios';
import OptionEdit from './OptionEdit'
import OptionDelete from './OptionDelete'
export default {
    name: 'Table',
    components: {
        OptionEdit,
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
            options: [],
            force: false
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
            this.getOptions();
        },
        getOptions() {
            let that = this;
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
