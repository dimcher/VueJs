<template>
    <td><button @click="deleteOption">DELETE</button></td>
</template>

<script>
import axios from 'axios';
export default {
    name: 'OptionDelete',
    props: {
        optionId: {
            type: Number
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
        deleteOption() {
            console.log("Delete");
            let that = this;
            axios
                .delete('https://services.metricsamsi.com/v1.0/dealers/Options/'+ that.optionId +'?apiKey='+ that.googleId)
                .then(function () {
                    this.refreshList();
                })
                .catch(e => {
                    that.errors.push(e);
                });
        },
        refreshList: function () {
            this.$emit('refreshMe');
        }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
</style>
