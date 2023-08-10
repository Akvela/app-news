<template>
  <div class="gallery">
    <div class="card" v-for="news in newsList" :key="news.code">
      <img v-if="news.image" :src="news.image" :alt="news.name" class="card__image"/>
      <div class="card__info">
        <p class="card__date">
          <span class="card__date-span">{{ setDate(news.date)[0] }}</span>
          <span>{{ setDate(news.date)[1] }}</span>
          <span>{{ setDate(news.date)[2] }}</span>
        </p>
        <h2 class="card__title">{{ news.name }}</h2>
        <p class="card__news">{{ news.previewText }}</p>
        <span class="card__label">{{ news.type.value }}</span>
      </div>
    </div>
  </div>
  <button v-if="showLoadMore" @click="loadMore" class="button">Загрузить еще</button>
</template>

<script>
  import moment from 'moment';

  export default {
    data() {
      return {
        newsList: [],
        currentPage: 1,
        totalPages: 1,
      };
    },
    computed: {
      showLoadMore() {
        return this.currentPage < this.totalPages;
      },
    },
    methods: {
      async fetchNews(page) {  
        try {
          const response = await fetch(`http://flems.github.io/test/api/news/${page}/`);
          const data = await response.json();
          return data;
        } catch (error) {
          console.error('Error fetching news:', error);
          return [];
        }
      },

      async loadMore() {
        this.currentPage++;
        const newData = await this.fetchNews(this.currentPage);
        this.newsList = [...this.newsList, ...newData.items];
      },

      setDate(date) {
        const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'] 
        const dateNews = new Date(moment.unix(date).utc());
        return `${dateNews.getDate()} ${months[dateNews.getMonth()]} ${dateNews.getFullYear()}`.split(' ')
      }
    },

    async mounted() {
      const initialData = await this.fetchNews(this.currentPage);
      if (initialData) {
        this.newsList = initialData.items;
        this.totalPages = initialData.nav.total;
      }
    },
  };
</script>

<style>
  .gallery {
    display: grid;
    margin: 66px 0 72px;
    grid-template-columns: repeat(3, 536px);
    gap: 48px;
    justify-content: center;
  }

  .card {
    width: 536px;
    border-radius: 16px;
    border: 1px solid #0F62FE;
    display: flex;
    flex-direction: column;
  }

  .card__image {
    margin: -1px 0 -16px -1px;
    width: 537px;
    height: 250px;
    border-radius: 16px 16px 0px 0px;

  }

  .card__date {
    margin: 16px 0;
    font-size: 15px;
    font-weight: 700;
    line-height: 17px;
    letter-spacing: -0.01em;
    color: #A1A7B5;
    display: grid;
    grid-template-columns: 44px 62px;
    grid-template-rows: 1fr 1fr;
    height: 36px;
    width: 110px;
    gap: 4px;
  }
   
  .card__date-span {
    font-size: 36px;
    font-weight: 400;
    grid-row: 1 / 3;
    align-self: center;
    text-align: center;
  }
  
  .card__info {
    padding: 32px;
    position: relative;
    height: 100%;
  }

  .card__title {
    font-size: 22px;
    font-weight: 400;
    color: #0C5BEF;
  }
  
  .card__news {
    font-size: 20px;
    font-weight: 400;
    line-height: 26px;
    color: #222327;
    margin-top: 16px;
    margin-bottom: 68px;
  }
  
  .card__label {
    background: #F0F6FE;
    height: 28px;
    padding: 4px 16px;
    border-radius: 360px;
    font-size: 14px;
    font-weight: 400;
    display: inline-block;
    position: absolute;
    bottom: 29px;
    left: 31px;
  }
  
  .button {
    display: block;
    width: 203px;
    height: 56px;
    cursor: pointer;
    font-size: 20px;
    font-weight: 600;
    text-align: center;
    color: #002DBF;
    margin: 0 auto;
    border-radius: 10px;
    border: 1px solid #002DBF;
    background: transparent;
  }

  @media screen and (max-width: 1750px) {
    .gallery {
      grid-template-columns: repeat(2, 536px);
    }
  }
  
  @media screen and (max-width: 1150px) {
    .gallery {
      grid-template-columns: repeat(2, 400px);
    }
    .card {
      width: 400px;
    }

    .card__image {
      width: 401px;
    }

    .card__news {
      margin-bottom: 40px;
    }
  }

  @media screen and (max-width: 890px) {
    .gallery {
      grid-template-columns: 536px;
    }

    .card {
      width: 536px;
    }

    .card__image {
      width: 537px;
    }
  }

  @media screen and (max-width: 574px) {
    .gallery {
      grid-template-columns: 300px;
    }

    .card {
      width: 300px;
    }

    .card__info {
      padding: 15px;
    }

    .card__image {
      width: 301px;
    }

    .card__title {
      font-size: 18px;
    }

    .card__news {
      font-size: 16px;
      margin-bottom: 60px;
    }
  }
</style>
