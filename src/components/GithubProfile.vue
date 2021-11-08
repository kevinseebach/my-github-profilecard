<template lang="html">
  <div class="github-card">
      <div class="header">
          <a class="avatar" :href="profile.html_url" target="_blank">
            <img :src="profile.avatar_url">
            <strong v-if="profile.name" class="dblock">{{profile.name}}</strong>
            <span>@{{profile.login}}</span>
            <small v-if="profile.location" class="dblock">{{profile.location}}</small>
          </a>
      </div>
      <div v-if="profile.bio" id="bio">
          {{profile.bio}}
      </div>
      <div class="status">
          <div>
              <a :href="profile.repos_url" target="_blank">
              <strong>{{profile.public_repos}}</strong>
              Repos
              </a>
          </div>
          <div>
              <a :href="'https://gist.github.com/'+profile.login" target="_blank">
              <strong>{{profile.public_gists}}</strong>
              Gists
              </a>
          </div>
          <div>
              <a :href="profile.followers_url" target="_blank">
              <strong>{{profile.followers}}</strong>
              Followers
              </a>
          </div>
          <div>
              <a :href="profile.html_url+'?tab=following'" target="_blank">
              <strong>{{profile.following}}</strong>
              Following
              </a>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      profile:{}
    }
  },
  props: {
      username: {
        type: String,
        required: true,
      }
  },
  mounted: function() {
    fetch(`https://api.github.com/users/`+this.username)
            .then((res) => this.profile = res.json())
            .then((data) => { this.profile = data;})
  }
}
</script>

<style lang="css" scoped>
.github-card .header{
  width:100%;
  display:block;
}
.dblock{
  display:block
}
#bio{
  width:100%;
  display:block;
  padding-top:10px;
  padding-bottom:10px;
}
.github-card {
    border: 1px solid #eaeaea;
    border-radius: 5px;
    padding: 8px 8px 0;
    background: #f4f4f4;
    color: #555;
    position: relative;
    width: 384px;
}
.github-card strong {
    display: block;
    color: #292f33;
    font-size: 16px;
    line-height: 1.6;
}
.github-card a {
    color: #707070;
    text-decoration: none;
}
.github-card div.status {
    text-transform: uppercase;
    font-size: 12px;
    color: #707070;
    width: 100%;
    margin-top: 15px;
    margin-bottom: 15px;
    padding-top:10px;
    width: 100%;
    display: flex;
    align-items: center;
    align-content: center;
    border-top : 2px solid #ccc;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
}

.github-card .status div {
    padding: 4px 18px;
    border-left: 1px sodivd #eee;
}

.github-card .footer {
  width: 100%;
  display: block;
  font-size: 12px;
  font-weight: 700;
  padding: 11px 0 10px;
  color: #646464;
}

.avatar img{
  max-width: 150px;
  border-radius: 25px;
  box-shadow: inset 0 3px 6px rgba(0,0,0,0.16), 0 4px 6px rgba(0,0,0,0.45);
}

</style>
