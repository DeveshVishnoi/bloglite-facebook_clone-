<template >
  <div>
    <header></header>
    <div class="header">
      <div class="header__left">
        <img src="/src/assets/images.jfif" alt="" />
        <div class="header__input">
          <span class="material-icons"> search </span>
          <input type="text" placeholder="Search Facebook" id="search_name" />
        </div>
        <div class="header__input">
          <button class="search" v-on:click="search">Search</button>
          <!-- <span class="material-icons"> search </span>
        <input type="text" placeholder="Search Facebook" /> -->
        </div>
      </div>

      <div class="header__right">
        <router-link to="/feed">
          <button class="btns">Feed</button>
        </router-link>
        <button class="btns red" v-on:click="logout"><i class="fa fa-sign-out" style="font-size:15px"></i>  Log Out</button>
        <div class="header__info">
          <router-link :to="'/' + this.user_id + '/profile'"
            ><div class="header__info">
              <img
                class="user__avatar"
                src="data:image/png;base64,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"
                alt=""
              />
              <h4>{{ username }}</h4>
            </div></router-link
          >
        </div>

        <!-- <span class="material-icons"> forum </span>
    <span class="material-icons"> notifications_active </span>
    <span class="material-icons"> expand_more </span> -->
      </div>
    </div>

    <div class="containerdp">
      <div class="wrapper">
        <section class="post">
          <button v-on:click="feed" style="float: right">
            <i class="fa fa-close" style="font-size: 15px"></i>
          </button>
          <header>Create Post</header>

          <div class="form">
            <div class="content">
              <img class="imgDp" :src="this.imageDP" alt="logo" />
              <div class="details">
                <a style="text-decoration: none">{{ username }}</a>
              </div>
            </div>
            <hr />
            <textarea
              v-model="post_desc"
              placeholder="What's on your mind, BlogLite "
              spellcheck="false"
              required
            ></textarea>
            <div class="theme-emoji">
              <img :src="imageurl" class="ap" v-if="imageurl" alt="theme" />
              <!-- 
                  <img src="icons/smile.svg" alt="smile"><span class="dropdown">
                <button  class="dropbtn">
                  Dropdown
                </button>
                <div id="myDropdown" class="dropdown-content">
                  <router-link :to="'/' + post.post_id + '/edit-post'">Edit</router-link>
                  <button v-on:click="del_post(post.post_id)">Delete</button>
                  <a href="#">Link 3</a>
                </div>
              </span> -->
            </div>
            <div class="options">
              <p>Add to Your Post</p>
              <input id="f_input" type="file" @change="handleImageUpload" />
            </div>
            <button v-on:click="addPost">Post</button>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import header from "./header.vue";
export default {
  components: {
    header,
  },
  name: "add_post",
  data() {
    return {
      link: "https://devbook-t6cy.onrender.com",
      user_id: JSON.parse(localStorage.getItem("user_info")).user_id,
      imageurl: "",
      post_desc: "",
      imageDP: localStorage.getItem("dp"),
      username:
        JSON.parse(localStorage.getItem("user_info")).firstname +
        " " +
        JSON.parse(localStorage.getItem("user_info")).lastname,
    };
  },
  methods: {
    handleImageUpload(event) {
      const file = event.target.files[0];
      // console.log(file.name);
      const reader = new FileReader();
      reader.onload = (event) => {
        this.imageurl = event.target.result;
        // console.log(this.imageurl);
        // localStorage.setItem('DP',this.imageurl)
      };
      reader.readAsDataURL(file);
    },

    feed() {
      this.$router.push({ name: "hello" });
    },
    logout() {
      // this.$store.commit('token_mutate', "");
      localStorage.clear();
      this.$router.replace({ name: "Login" });
    },

    addPost() {
      fetch(`${this.link}/api/${this.user_id}/add`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          sar_babu: localStorage.getItem("token"),
        },
        body: JSON.stringify({
          post_desc: this.post_desc,
          post_image: this.imageurl,
        }),
      })
        .then((res) => {
          if (res.ok) {
            return res.json();
          } else if (res.status === 401) {
            throw new Error();
            // console.log(res);
          } else {
            // console.log(res);
          }
        })
        .then((data) => {
          console.log(data);
          // this.get_user_details();
          this.$router.push({ name: "hello" });
        })
        .catch((err) => this.$router.replace({ name: "Login" }));
    },
    search() {
      var name = document.querySelector("#search_name");
      console.log(name.value);
      this.$router.push({ path: `/${name.value}/search_user` });
    },
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}
.ap {
  width: 200px;
  height: 200px;
  overflow: scroll;
  max-height: 200px;
}

.imgDp {
  vertical-align: middle;
  width: 40px;
  height: 40px;
  border-radius: 50%;
}
body {
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  /* background: linear-gradient(#00C6FF, #0078FF);*/
}
::selection {
  color: #fff;
  background: #1a81ff;
}
.containerdp {
  width: 500px;
  height: fit-content;

  margin: auto;
  margin-top: 35px;
  overflow: hidden;
  background: #fff;
  border-radius: 10px;
  transition: height 0.2s ease;
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.12);
}
.theme-emoji {
  overflow-y: hidden;
}
.containerdp.active {
  height: 590px;
}
.containerdp .wrapper {
  width: 1000px;
  display: flex;
}
.containerdp .wrapper section {
  width: 410px;
  background: #fff;
}
.containerdp img {
  cursor: pointer;
}
.containerdp .post {
  transition: margin-left 0.18s ease;
}
.containerdp .active .post {
  margin-left: -500px;
}
.post header {
  font-size: 22px;
  font-weight: 600;
  padding: 17px 0;
  text-align: center;
  border-bottom: 1px solid #bfbfbf;
}
.post .form {
  margin: 6px 25px;
}
.post .form .content,
.audience .list li .column {
  display: flex;
  align-items: center;
}
.post .form .content {
  margin-bottom: 5px;
}
.post .form .content img {
  cursor: default;
  max-width: 52px;
}
.post .form .content .details {
  margin: -3px 0 0 12px;
}
.form .content .details p {
  font-size: 17px;
  font-weight: 500;
}
.content .details .privacy {
  display: flex;
  height: 25px;
  cursor: pointer;
  padding: 0 10px;
  font-size: 11px;
  margin-top: 3px;
  border-radius: 5px;
  align-items: center;
  max-width: 98px;
  background: #e4e6eb;
  justify-content: space-between;
}
.details .privacy span {
  font-size: 13px;
  margin-top: 1px;
  font-weight: 500;
}
.details .privacy i:last-child {
  font-size: 13px;
  margin-left: 1px;
}
.form :where(textarea, button) {
  width: 100%;
  outline: none;
  border: none;
}
.form textarea {
  resize: none;
  font-size: 18px;
  margin-top: 30px;
  min-height: 60px;
}
.form textarea::placeholder {
  color: #858585;
}
.form textarea:focus::placeholder {
  color: #b3b3b3;
}
.form :where(.theme-emoji, .options) {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.theme-emoji img:last-child {
  margin: auto;
}
.form .options {
  height: 37px;
  margin: 15px 0;
  padding: 0 15px;
  border-radius: 7px;

  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}
.form .options :where(.list, li),
.audience :where(.arrow-back, .icon, li .radio) {
  display: flex;
  align-items: center;
  justify-content: center;
}
.form .options p {
  color: #595959;
  font-size: 15px;
  font-weight: 500;
  cursor: default;
}
.form .options .list {
  list-style: none;
}
.options .list li {
  height: 42px;
  width: 42px;
  margin: 0 -1px;
  cursor: pointer;
  border-radius: 50%;
}
.options .list li:hover {
  background: #f0f1f4;
}
.options .list li img {
  width: 23px;
}
.form button {
  height: 40px;
  color: #fff;
  font-size: 18px;
  font-weight: 500;
  cursor: pointer;
  color: #bcc0c4;
  cursor: no-drop;
  border-radius: 7px;
  background: #e2e5e9;
  transition: all 0.3s ease;
}
.form textarea:valid ~ button {
  color: #fff;
  cursor: pointer;
  background: #4599ff;
}
.form textarea:valid ~ button:hover {
  background: #1a81ff;
}
.container .audience {
  opacity: 0;
  transition: opacity 0.12s ease;
}
.container.active .audience {
  opacity: 1;
}
.audience header {
  padding: 17px 0;
  text-align: center;
  position: relative;
  border-bottom: 1px solid #bfbfbf;
}
.audience header .arrow-back {
  position: absolute;
  left: 25px;
  width: 35px;
  height: 35px;
  cursor: pointer;
  font-size: 15px;
  color: #747474;
  border-radius: 50%;
  background: #e4e6eb;
}
.audience header p {
  font-size: 22px;
  font-weight: 600;
}
.audience .content {
  margin: 20px 25px 10;
}
.audience .content p {
  font-size: 17px;
  font-weight: 500;
}
.audience .content span {
  font-size: 14px;
  color: #65676b;
}
.audience .list {
  margin: 15px 16px 20px;
  list-style: none;
}
.audience .list li {
  display: flex;
  cursor: pointer;
  margin-bottom: 5px;
  padding: 12px 10px;
  border-radius: 7px;
  align-items: center;
  justify-content: space-between;
}
.list li.active,
.audience .list li.active:hover {
  background: #e5f1ff;
}
.audience .list li:hover {
  background: #f0f1f4;
}
.audience .list li .column .icon {
  height: 50px;
  width: 50px;
  color: #333;
  font-size: 23px;
  border-radius: 50%;
  background: #e4e6eb;
}
.audience .list li.active .column .icon {
  background: #cce4ff;
}
.audience .list li .column .details {
  margin-left: 15px;
}
.list li .column .details p {
  font-weight: 500;
}
.list li .column .details span {
  font-size: 14px;
  color: #65676b;
}
.list li .radio {
  height: 20px;
  width: 20px;
  border-radius: 50%;
  position: relative;
  border: 1px solid #707070;
}
.list li.active .radio {
  border: 2px solid #4599ff;
}
.list li .radio::before {
  content: "";
  width: 12px;
  height: 12px;
  border-radius: inherit;
}
.list li.active .radio::before {
  background: #4599ff;
}
</style>
