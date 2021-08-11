<template>
    <div class="actions">
        <button>NEW</button>
        <button>SAVE</button>
        <button>DELETE</button>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Actions',
    data: () => {
        return {
            errors: []
        }
    },
    props: {
    },
    created: function() {
        this.getAccounts()
    },
    methods: {
        getAccounts() {
            let that = this;
            axios
                .get("https://services.metricsamsi.com/v1.0/dealers/Accounts/Google?apiKey=81c14de2-6891-461b-9ea6-3ed218675b8f")
                .then(function (response) {
                    that.accounts = response.data.data;
                })
                .catch(e => {
                    this.errors.push(e);
                });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
</style>
