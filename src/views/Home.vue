<template>
  <div class="home">
    <vs-row justify="center">
      <vs-col lg="3" sm="4" xs="12">
        <h1>VUE APP NEWS</h1>
      </vs-col>
    </vs-row>
    <vs-row justify="center">
      <vs-col lg="3" sm="4" xs="12">
        <vs-input block state="primary" success v-model="search" placeholder="Search...">
          <template #icon>
            <i class='bx bx-search'></i>
          </template>
        </vs-input>
      </vs-col>
    </vs-row>
    <vs-row>
      <vs-col lg="3" sm="4" xs="12" v-for="(article, index) in news" :key="index">
        <vs-card @click="openUrl(article.url)" >
          <template #title>
            <h3>{{ article.texto }}</h3>
          </template>
          <template #img>
            <img :src="article.img" alt="">
          </template>
          <template #text>
            <p></p>
          </template>
          <template #interactions>
            <vs-button danger icon>
              <i class='bx bx-heart'></i>
            </vs-button>
            <vs-button class="btn-chat" shadow primary>
              <i class='bx bx-chat' ></i>
              <span class="span">
                54
              </span>
            </vs-button>
          </template>
        </vs-card>
      </vs-col>
    </vs-row>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Home',
  data() {
    return {
      news: [
        {
          img: '',
          url: '',
          texto: ''
        }
      ],
      search: ''
    }
  },
  mounted() {
    this.getNews();
  },
  methods: {
    getNews() {
      axios.get('https://america-news.herokuapp.com/scraping').then(response => {
        this.news = response.data
      }).catch(error => console.log(error));
    },
    openUrl(url) {
      window.location.href = url
    }
  }
}
</script>

<style>
  .vs-card-content {
    margin: 0px 15px 15px 0px;
  }

  .vs-input-parent {
    margin-bottom: 20px;
  }
</style>
