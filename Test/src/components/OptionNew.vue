<template>
    <div>
        <div class="sign">Option Editor</div>
        <div class="sign">New Option</div>
        <p><input type="text" name="googleId" /></p>
        <button :name="googleId" @click="getGoogleId">SUBMIT</button>
    </div>
</template>

<script>
export default {
    name: 'OptionNew',
    props: {
    },
    data: () => {
        return {
            googleId: ''
        }
    },
    methods: {
        getGoogleId: function () {
            const id = document.querySelector("input[name=googleId]").value;
            this.$emit('getGoogleId', id);
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
