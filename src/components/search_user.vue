<template>
    <div>
        <div class="header">
            <div class="header__left">
              <img
			src="/src/assets/images.jfif"
            alt=""
        />
              <div class="header__input">
                <span class="material-icons"> search </span>
                <input type="text" placeholder="Search Facebook" id="search_name"/>
              </div>
              <div class="header__input">
                <button class="search" v-on:click="search">Search</button>
                <!-- <span class="material-icons"> search </span>
                <input type="text" placeholder="Search Facebook" /> -->
                </div>
            </div>
      
            <div class="header__right">
                <router-link to="/feed">
                    <button class="btns">
                      Feed
                    </button>
                  </router-link>
                  <button class="btns  red" v-on:click="logout">
                    <i class="fa fa-sign-out" style="font-size:15px"></i>  Log Out
                    </button>
              <div class="header__info">
                <router-link :to="'/' +this.user_id+ '/profile'"
                  ><div class="header__info">
                    <img
                      class="user__avatar"
                      src="data:image/png;base64,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"
                      alt=""
                    />
                    <h4>{{username}}</h4>
                  </div></router-link
                >
              </div>
      
              <!-- <span class="material-icons"> forum </span>
            <span class="material-icons"> notifications_active </span>
            <span class="material-icons"> expand_more </span> -->
            </div>
          </div>
        <div class="row-u">
        
          <div class="column-u" v-for="(user, index) in users" :key="index">
            
                <div class="cards">
                    <img :src="user.dp[0].dp_name" alt="Avatar" style="" v-if="user.dp[0].dp_name">
                    <div class="container-u">
                        <router-link :to="'/' + user.user_id + '/profile_frnd'" ><h4><b>{{user.firstname}} {{user.lastname}}</b></h4> </router-link>
                        <p class="fu">
                          <button class="he">All Post :{{user.posts.length}}</button>
                          <button class="he">Followers :{{user.followed.length}}</button>
                          <button class="he">Following :{{user.followers.length}}</button>
                       
                        </p> 
                      <p class="fu">
                        <button class="button" v-on:click="folloow(user.user_id)">Follow</button>
                        <button class="button" v-on:click="unfolloow(user.user_id)">Unfollow</button>
                      </p> 
                    </div>
                  </div>
            
          </div>
          
          
          
          
          
          
          

      </div>
    </div>
    
    

</template>

<script>

export default{
    name:'all_user',
    data(){
        return {
            isActive:false,
            name:this.$route.params.str,
            user_id:JSON.parse(localStorage.getItem('user_info')).user_id,
            username:JSON.parse(localStorage.getItem("user_info")).firstname + " " + JSON.parse(localStorage.getItem("user_info")).lastname,
            users:[],
            link:"https://devbook-t6cy.onrender.com"
        }
    },
    methods:{
      logout(){
            // this.$store.commit('token_mutate', "");
            localStorage.clear();
            this.$router.replace({ name: "Login" });
        },
        
        folloow(id){
            console.log(id);
                fetch(`https://devbook-t6cy.onrender.com/follow/${this.user_id}` , {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                            // "Access-Control-Allow-Origin": window.location.origin,
                            "sar_babu": localStorage.getItem("token"),
                        },      
                            
                body: JSON.stringify({  
                    'follower_id':this.user_id,
                    "followed_id":id
                    
                })
            })
                .then((res) => {
                if (res.ok) {
                    return res.json();
                } else if (res.status === 401) {
                    throw new Error();
                    // console.log(res);
                }
                else{
                    // console.log(res);

                }
                })
                .then((data) => {
                console.log(data);
                this.det_search_people();
                
                })
                .catch((err) => console.log(err));


	} ,
    unfolloow(id){
		fetch(`https://devbook-t6cy.onrender.com/unfollow/${this.user_id}` , {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    // "Access-Control-Allow-Origin": window.location.origin,
                    "sar_babu": localStorage.getItem("token"),
                },      
					
        body: JSON.stringify({  
            'follower_id':this.user_id,
            "followed_id":id
            
        })
	})
         .then((res) => {
           if (res.ok) {
             return res.json();
           } else if (res.status === 401) {
             throw new Error();
             // console.log(res);
           }
           else{
             // console.log(res);

           }
         })
         .then((data) => {
           console.log(data);
           this.det_search_people();
		//    this.myfollowerslength = data.length;
		//    this.myfollowers = data
           // this.get_user_details();
        //    this.$router.push({ path: 'profile' });
         })
         .catch((err) => console.log(err));


	} ,
    search(){
        var name = document.querySelector('#search_name').value;
        console.log(name);
        this.$router.push({ path: `/${name.value}/search_user` });
    }

    ,
    det_search_people(){
      // var name = document.querySelector('#search_name');
      // console.log(name.value);
      fetch(`${this.link}/search/${this.name}`, {
                method: "GET",
                headers: { "sar_babu": localStorage.getItem("token"), },
            })
                .then((res) => {
                if (res.ok) {
                    return res.json();
                } else if (res.status === 401) {
                    throw new Error();
                }
                })
                .then((res) => {
                // (this.email_id = res.email_id),
                    // (this.username = res.username),
                    // (this.password = res.password),
                    // (this.user_id = res.user_id),
                    // (this.posts.push(res));
                    if(res.length != 0){
                      this.users = res;
                      console.log(res);
                      console.log(this.users);
                    }
                    else{
                      alert("This name of the user  is not present in this Site!!!")
                      this.$router.push({name:'hello'})
                    }
                    
                    // this.posts[0] = this.posts[0].reverse();
                    console.log(res);
                    console.log(this.users);
                })
                .catch((err) => this.$router.push({ }));
        
        
    }




    },
    mounted(){
        // this.all_user();
        this.det_search_people();
    }
}

</script>
<style>
.column-u {
    float: left;
    width: 25%;
    padding: 0 10px;
  }

  
  
  .cards:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
  }
  

  .cards img{
    width:300px;
    height:200px;
  }
  .fu .button{
    margin:10px;
    padding:10px 10px;
    border-radius:5px ;
    border: none;
    background-color:rgb(169, 169, 241) ;
    color:blue;
    font-weight:15px ;
    cursor: pointer;
  }

  .fu button:hover{
    background-color:lightblue
  }


  .container-u {
    padding: 10px 16px;
  }
  
  /* Remove extra left and right margins, due to padding */
  .row-u {
    margin: 0 -5px;
    max-height: 615px;
    overflow:scroll;
}
  
  /* Clear floats after the columns */
  .row-u:after {
    content: "";
    display: table;
    clear: both;
  }
  
  /* Responsive columns */
  @media screen and (max-width: 600px) {
    .column-u {
      width: 100%;
      display: block;
      margin-bottom: 20px;
    }
  }
  
  /* Style the counter cards */
 
  .cards {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    width:300px;
    border-radius: 5px;
    margin-top:20px;
    margin-left:10px;
    text-align: center;
    background-color: #f1f1f1;
  }
  
  img{
    border-radius: 5px 5px 0 0;
  }
  
</style>
