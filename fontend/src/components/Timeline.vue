<template>
  <div class="list-wrapper">
    <ul class="list-container" id="list-ul">
      <li v-for="item in items">
        <a v-link="{ name: 'post', params: {title: item.title}}">
          <p class="list-title">{{item.title}}</p>
          <p class="list-updated">{{item.time.day}}</p>
          <p class="list-abstract">{{item.abstract}}</p>
        </a>
      </li>
    </ul>
  </div>
</template>

<script type="text/babel">
  import {getPostsList, updateHeadline} from '../vuex/actions'

  export default {
    vuex: {
      // 该 getter 函数将会把仓库的 `store.postsList.postsList` 绑定为组件的 `items`
      getters: {
        items: function ({postsList}) {
          return postsList.postsList
        }
      },
      actions: {
        getPostsList: getPostsList,
        updateHeadline: updateHeadline
      }
    },
    created () {
      this.getPostsList()
      this.updateHeadline('时间线')
    }
  }
</script>

<style>
  .list-container li {
    border-bottom: 1px solid #eee;
  }

  .list-title {
    font-size: 2.6rem;
    font-weight: 400;
    color: #404040;
    margin-top: 0;
  }

  .list-abstract {
    font-size: 1.6rem;
    color: #919191;
    font-weight: 300;
  }

  .list-updated {
    font-family: "Comic Sans MS", curslve, sans-serif;
    font-size: 1.8rem;
    color: #8b8b8b;
    padding: 5px 0;
  }

  .list-container li a {
    padding: 1rem 1.5rem;
    display: block;
    transition: all .3s;
    margin: 0;
  }

  .list-container li a:hover {
    background-color: Rgba(0, 0, 0, .02);
  }

  @media screen and (max-width: 768px) {
    .list-title {
      font-size: 2.2rem;
    }

    .list-updated {
      font-size: 1.6rem;
    }
  }
</style>
