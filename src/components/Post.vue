<template>
  <div class="hello container mt-3">
    <ul class="list-unstyled">
      <div v-for="post in posts" class="row my-4">

        <div class="col text-center ">
          <h3 class="text-secondary">
            <svg width="24px" height="24px" viewBox="0 0 16 16" class="bi bi-arrow-up-square-fill" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
              <path fill-rule="evenodd" d="M2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2zm6.5 11.5a.5.5 0 0 1-1 0V5.707L5.354 7.854a.5.5 0 1 1-.708-.708l3-3a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1-.708.708L8.5 5.707V11.5z"/>
            </svg>
            <p>{{post.data.ups}}</p>
          </h3>
        </div>

        <div class="col-11">
          <li class="media">
            <img v-if="isImage(post.data.thumbnail)" :src="post.data.thumbnail" class="img-thumbnail mr-3" width="72" height="72">
            <img v-if="!isImage(post.data.thumbnail)" src="https://64.media.tumblr.com/4e3fc52c494de4a4be58a290086539e5/tumblr_mlkpkpSnXZ1s473u3o1_540.png" class="img-thumbnail mr-3" width="72" height="72">
              <div class="media-body">
                <a :href="post.data.url" target="blank"><h5 class="mt-0 mb-1">{{post.data.title}}</h5></a>
                  <p>
                    <span><button @click="post.showImg = !post.showImg"
                     v-if="isImage(post.data.thumbnail)" type="button" class="btn btn-light btn-sm mr-3"> <svg width="16px" height="16px" viewBox="0 0 16 16" class="bi bi-aspect-ratio" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" d="M0 3.5A1.5 1.5 0 0 1 1.5 2h13A1.5 1.5 0 0 1 16 3.5v9a1.5 1.5 0 0 1-1.5 1.5h-13A1.5 1.5 0 0 1 0 12.5v-9zM1.5 3a.5.5 0 0 0-.5.5v9a.5.5 0 0 0 .5.5h13a.5.5 0 0 0 .5-.5v-9a.5.5 0 0 0-.5-.5h-13z"/>
                        <path fill-rule="evenodd" d="M2 4.5a.5.5 0 0 1 .5-.5h3a.5.5 0 0 1 0 1H3v2.5a.5.5 0 0 1-1 0v-3zm12 7a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1 0-1H13V8.5a.5.5 0 0 1 1 0v3z"/>
                      </svg></button></span> 
                    Created {{formatDate(post.data.created_utc)}} by {{post.data.author}}
                  </p>
                  <div v-if="isImage(post.data.thumbnail) && post.showImg">
                    <img :src="post.data.thumbnail">
                  </div>
                  <span class="badge badge-dark btn-sm">{{post.data.num_comments}} comments</span>

              </div>
          </li>
        </div>

      </div>

    </ul>
  </div>
</template>

<script>

import {parseJSON, formatDistance, da} from 'date-fns'

export default {
  name: 'Post',
  data() {
    return {
      posts: [],
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      const url = 'https://www.reddit.com/r/xbox/.json';
      fetch(url).then(response => response.json()).then((result) => {
        result.data.children.forEach(child => {
          child.showImg = false;
        });
        this.posts = result.data.children;
      });
    },
    formatDate(date) {
      return formatDistance(parseJSON(date * 1000), new Date(), { addSuffix: true });
    },
    isImage(img) {
      return img.match(/\.(jpg|png|jpeg|bpm)$/);
    }
  },
};
</script>
