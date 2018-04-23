<template>
  <div class="container">
    <Dashboard>
      <Widget>
        <form @submit="addTweet" class="newTweet">
          <div class="newTweet__editorArea">
            <span 
              :class="tweetClassName">
              {{ newTweet.length }}/140
            </span>
            <textarea 
              v-model="newTweet"
              class="newTweet__editor" 
              placeholder="What's Happening?">
            </textarea>
          </div>
          <button 
            :disabled="isTweetInvalid"
            type="submit" 
            class="newTweet__envia">
            Tweet
          </button>
        </form>
      </Widget>
      <Widget>
        <TrendingTopics />
      </Widget>
    </Dashboard>
    <Dashboard position="center">
      <Widget>
        <div class="tweetsArea">
          <Tweet v-for="tweet in tweets" :key="tweet._id" :content="tweet.conteudo" :tweetInfo="tweet" /> 
        </div>
      </Widget>
    </Dashboard>
  </div>
</template>

<script>
import Header from '../components/Header.vue';
import Dashboard from '../components/Dashboard.vue';
import Widget from '../components/Widget.vue';
import Tweet from '../components/Tweet.vue';
import TrendingTopics from '../components/TrendingTopics.vue';

export default {
  name: 'Timeline',
  components: {
    Header,
    Dashboard,
    Widget,
    TrendingTopics,
    Tweet
  },
  data() {
    return {
      newTweet: '',
      tweets: [{"usuario":{"login":"omariosouto","nome":"Mario","sobrenome":"Souto","foto":"https://www.caelum.com.br/imagens/instrutores/fotos/mario-souto-120.jpg","email":"mario.souto@caelum.com.br"},"conteudo":"Neque instant #quisquam quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit.","likes":[{"usuario":{"login":"artdiniz"}}],"totalLikes":1,"_id":"O331kDvyUt2ACD8f","createdAt":"2018-04-22T11:38:45.590Z","updatedAt":"2018-04-22T11:38:45.590Z"},{"usuario":{"login":"vanessametonini","nome":"Vanessa","sobrenome":"Tonini","foto":"https://www.caelum.com.br/imagens/instrutores/fotos/vanessa-tonini-120.jpg","email":"vanessa.tonini@caelum.com.br"},"conteudo":"#Dasque instant quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit.","likes":[{"usuario":{"login":"omariosouto"}}],"totalLikes":1,"_id":"l0xs0h7kwv2r6kll","createdAt":"2018-04-22T11:38:45.590Z","updatedAt":"2018-04-22T16:38:22.538Z"},{"usuario":{"login":"marcobrunobr","nome":"Marco","sobrenome":"Bruno","foto":"https://www.caelum.com.br/imagens/instrutores/fotos/marco-bruno-120.jpg","email":"marco.bruno@caelum.com.br"},"conteudo":"Ipsum instant quisquam est qui #dolorem ipsum quia dolor #sit amet, consectetur, adipisci velit.","likes":[{"usuario":{"login":"vanessametonini"}},{"usuario":{"login":"omariosouto"}}],"totalLikes":2,"_id":"wHxm4X5iDtRMcQuN","createdAt":"2018-04-22T11:38:45.590Z","updatedAt":"2018-04-22T11:38:45.590Z"},{"usuario":{"login":"artdiniz","nome":"Artur","sobrenome":"Diniz","foto":"https://www.caelum.com.br/imagens/instrutores/fotos/artur-diniz-120.jpg","email":"artur.diniz@caelum.com.br"},"conteudo":"Daino instant quisquam est qui #dolorem ipsum quia dolor sit amet, consectetur, adipisci velit.","likes":[],"totalLikes":0,"_id":"x22C4iPV3tOsLToe","createdAt":"2018-04-22T11:38:45.590Z","updatedAt":"2018-04-22T11:38:45.590Z"}]
    }
  },
  methods: {
    addTweet (event) {
      event.preventDefault();

      if(this.isTweetInvalid || this.newTweet.length === 0) {
        console.error(`Warning: Tweet must not be empty and contain less than 140 characters. Current length: ${this.newTweet.length}`);
      } else {
        fetch('http://twitelum-api.herokuapp.com/tweets', {
          method: 'POST',
          body: JSON.stringify(
            { conteudo: this.newTweet, login: 'vanessametonini' }
          )
        })
        .then( response => response.json() )
        .then( newTweet => {
          this.tweets = [newTweet, ...this.tweets];
          newTweet = '';
        } )
      }
    },
    validateNewTweet() {
      return this.newTweet.length < 0 || this.newTweet.length > 240 ? true : false;
    }
  },
  computed: {
    tweetClassName() {
      return `newTweet__status  ${ this.validateNewTweet() ? ' newTweet__status--invalido' : ''}`;
    },
    isTweetInvalid() {
      return this.newTweet.length < 0 || this.newTweet.length > 240 ? true : false;
    }
  }
}
</script>

<style>
.container {
  box-sizing: border-box;
}
.newTweet:after {
  content: "";
  clear: both;
  width: 100%;
  display: block;
}

.newTweet__editor {
  width: 100%;
  transition: height .2s;
  border: 1px solid #ABE6F8;
  border-radius: 4px;
  resize: none;
  padding: 8px;
  height: 40px;
  font-size: 11px;
}
.newTweet__editor:not(:empty),
.newTweet__editor:focus {
  height: 80px;
  box-shadow: 0 0 0 1px #ABE6F8;
  outline: 0;
}

.newTweet__status {
  float: right;
  font-size: 14px;
  margin-bottom: 7px;
}
.newTweet__status--invalido {
  color: red;
}

.newTweet__envia {
  float: right;
  color: white;
  background-color: #58CEF2;
  border-color: transparent;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  font-weight: bold;
  line-height: 20px;
  padding: 5px 11px;
  position: relative;
  text-align: center;
  white-space: nowrap;
  margin-top: 3px;
}
/* iconHeart */
.iconHeart {
  fill: #cccccc;
}
.iconHeart--active {
  fill: #be1931;
}
/* icon */
.icon {
  margin-right: 3px;
}
.icon--small {
  width: 15px;
  height: 15px;
}
/* btn */
.btn {
  padding: 3px;
  display: inline-flex;
  justify-content: center;
  align-items: flex-end;
}
.btn--clean {
  border: 0;
  background: none;
}
</style>
