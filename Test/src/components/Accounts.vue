<template>
    <select name="account" :value="account" @change="changeAccount($event)">
        <option 
            v-for="(obj, index) in accounts" 
            :key="`account-${index}`"
            :value="obj.googleId" 
        >{{obj.viewName}}</option>
    </select>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Accounts',
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
            errors: [],
            accounts: []
        }
    },
    created: function() {
        this.getAccounts()
    },
    methods: {
        getAccounts() {
            let that = this;
            axios
                .get("https://services.metricsamsi.com/v1.0/dealers/Accounts/Google?apiKey="+ that.googleId)
                .then(function (response) {
                    that.accounts = response.data.data;
                })
                .catch(e => {
                    this.errors.push(e);
                });
        },
        changeAccount(event) {
            this.$emit('getAccount', event.target.selectedOptions[0].value);
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
