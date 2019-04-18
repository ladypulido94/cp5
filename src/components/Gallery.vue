<template>
    <div>
        <div class="image" v-for="photo in photos" v-bind:key="photo._id">
            <img :src="photo.path" />
            <p class="photoTitle">Title: {{photo.title}}</p>
            <p>Season: {{photo.description}}</p>
            <p class="photoDate">
                <span v-if="photo.user && photo.user.name">{{photo.user.name}}, </span>
                {{formatDate(photo.created)}}
            </p>
            <button @click="deletePhoto()">Delete</button>
            <button @click="editPhoto()">Edit</button>
        </div>
    </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'Gallery',
  props: {
    photos: Array
        },
        methods: {
            formatDate(date) {
                if (moment(date).diff(Date.now(), 'days') < 15)
                    return moment(date).fromNow();
                else
                    return moment(date).format('d MMMM YYYY');
            },
            async deletePhoto() {
                await this.$store.dispatch("deletePicture", { id: this.$route.params.id });
            },
            async editPhoto() {
                await this.$store.dispatch("editPicture", { id: this.$route.params.id });
            }
        }
}
</script>

<style scoped>
    .photoTitle {
        margin: 0px;
        font-size: 1.2em;
        color: #91818A;
    }

    .photoDate {
        margin: 0px;
        font-size: 0.9em;
        font-weight: normal;
        color: #91818A;
    }

    p {
        margin: 0px;
        color: #91818A;
    }

    .image {
        margin: 0 0 1.5em;
        display: inline-block;
        width: 100%;
    }

        .image img {
            max-width: 600px;
            max-height: 600px;
            image-orientation: from-image;
        }

</style>