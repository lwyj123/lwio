<template>
  <div class="article-content">
    <h1 class="article-title">{{ title }}</h1>
    <author-bar />
    <div class="article-html" v-html="contentHTML">
    </div>
    <ul class="article-tags">
      <li v-for="(tag, index) in tags" :key="index">
        {{ tag }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import AuthorBar from './AuthorBar.vue'
import marked from 'marked'
// import { getArticle } from '@/api/article'
@Component({
  name: 'ArticleContent',
  components: {
    AuthorBar
  }
})
export default class ArticleDetailPage extends Vue {
  public tags?: string[]
  public title = 'Loading...'
  public contentMD = 'Loading'

  get contentHTML () {
    return marked(this.contentMD, { sanitize: true })
  }
  public async mounted () {
    // const res = await getArticle(this.$route.params.articleId)
    // this.title = res.title
    // this.contentMD = res.content_md
    // this.tags = res.tags
    this.title = 'You Might Not Need Redux'
    this.contentMD = `People often choose Redux before they need it. “What if our app doesn’t scale without it?” Later, developers frown at the indirection Redux introduced to their code. “Why do I have to touch three files to get a simple feature working?” Why indeed!

None of these limitations are required to build an app, with or without React. In fact these are pretty strong constraints, and you should think carefully before adopting them even in parts of your app.`
    this.tags = ['keke', 'React']
  }
}
</script>

<style rel="stylesheet/scss" lang="scss">
.article-content {
  h1.article-title {
    margin: 0;
    padding: 16px 0 0 0;

    font-family: medium-content-title-font,Georgia,Cambria,"Times New Roman",Times,serif;
    font-weight: 400;
    font-style: normal;
    letter-spacing: 0;
    font-size: 42px;
    line-height: 1.04;
    letter-spacing: -.015em;
  }
  .article-html {
    margin-bottom: 30px;
    h1 {
      font-size: 35px;
    }
    h2 {
      font-size: 30px;
    }
    h3 {
      font-size: 26px;
    }
    h4,h5,h6 {
      font-size: 22px;
    }
    p {
      margin-top: 10px;

      font-weight: 400;
      font-style: normal;
      font-size: 21px;
      line-height: 1.58;
      letter-spacing: -.003em;
    }
    blockquote {
      margin-top: 29px;

      font-weight: 400;
      font-style: italic;
      font-size: 21px;
      line-height: 1.58;
      letter-spacing: -.003em;
    }
  }
  ul.article-tags {
    li {
      display: inline-block;
      position: relative;
      border: none;
      padding: 8px 10px;
      font-size: 13px;
      margin-right: 10px;
      border-radius: 5px;
      color: rgba(0,0,0,.68);
      background: rgba(0,0,0,.05);
      
      &:hover {
        cursor: pointer;
        background: rgba(0,0,0,.1);
        color: rgba(0,0,0,.68);
      }
    }
  }
}
</style>
