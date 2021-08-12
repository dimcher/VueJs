<template>
<div :key="action.type">
    <div v-if="action.type === 'EDIT'">
        <OptionEdit :option="action.option" @doAction="doAction" :keys="keys" :head="head" :googleId="googleId" />
    </div>
    <div v-else-if="action.type === 'NEW'">
        <OptionNew @soAction="doAction" />
    </div>
    <div v-else>
        <table>
            <tr>
                <th v-for="(value, index) in keys" :key="`thead-${index}`">{{head[value]}}</th>
                <th colspan="2">Actions</th>
            </tr>
            <tbody :key="JSON.stringify(options)">
                <tr v-for="(rv, ri) in options" :key="`row-${ri}`">
                    <td v-for="(cv, vi) in keys" :key="`value-${vi}`">{{rv[cv]}}</td>
                    <BtnOptionEdit :optionId="rv['rooftopGoogleOptionId']" :option="rv" @doAction="doAction" />
                    <BtnOptionDelete :optionId="rv['rooftopGoogleOptionId']" :googleId="googleId" @refreshList="refreshMe" />
                </tr>
            </tbody>
        </table>
    </div>
</div>
</template>

<script>
import axios from 'axios';
import BtnOptionEdit from './BtnOptionEdit'
import BtnOptionDelete from './BtnOptionDelete'
import OptionEdit from './OptionEdit'
import OptionNew from './OptionNew'

export default {
    name: 'Table',
    components: {
        BtnOptionEdit,
        BtnOptionDelete,
        OptionEdit,
        OptionNew
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
            action: {}
        }
    },
    watch: {
        account: function() {
            this.getOptions();
        },
    },
    created: function() {
        this.getOptions();
    },
    methods: {
        refreshMe() {
            this.getOptions();
        },
        doAction(action) {
            this.action = action;
        },
        getOptions() {
            let that = this;
            axios
                .get('https://services.metricsamsi.com/v1.0/dealers/Options/'+ that.account +'?apiKey='+ that.googleId)
                .then(function (response) {
                    that.options = response.data.data;
//                    console.log(that.options[0]);
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
    th {background-color: silver}
</style>
