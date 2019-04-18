<template>
    <div class="home">

        <div v-if="user">
            <gallery :photos="photos" />
        </div>

        <div v-else>
            <h3>I have a treasure in this page, and I'm sure this is the best thing ever.</h3>
            <p>If you want to know and help me collect more treasures? LOG IN NOOOOOOOOOW!!</p>
            <p>Hopefully you will like my reasure :)</p>

        </div>
    </div>
</template>

<script>
    // @ is an alias to /src
    import Gallery from '@/components/Gallery.vue'

    export default {
        name: 'home',
        components: {
            Gallery
        },
        computed: {
            user() {
                return this.$store.state.user;
            },
            photos() {
                return this.$store.state.photos;
            }
        },
        async created() {
            await this.$store.dispatch("getUser");
            await this.$store.dispatch("getAllPhotos");
        },
    }
</script>
