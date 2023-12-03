<template>
  <div class="app1" :class="{ 'dark-mode': isDarkMode , 'modal_open': isModalOpen }" >
    <lamp></lamp>
    <Menu></Menu>
    <div class="book">
      <div class=" post-cont post-cont1">
        <h1>Посты</h1>
        <div v-for="(post, index) in firstColumn" :key="post.id" class="post">
          <h3 class="post-title">{{ post.title }}</h3>
          <p>{{ post.body }}</p>
          <div class="btn">
            <button @click="openModal(post.id)">Показать комментарии к посту</button>
            <button @click="userpage(post.userId)">Перейти к пользователю</button>
          </div>
        </div>
      </div>
      <div class="sq"></div>
      <div class="post-cont post-cont2">
        <h1 class="post2">Посты</h1>
        <div v-for="(post, index) in secondColumn" :key="post.id" class="post post2">
          <h3 class="post-title">{{ post.title }}</h3>
          <p>{{ post.body }}</p>
          <div class="btn">
            <button @click="openModal(post.id)">Показать комментарии к посту</button>
            <button @click="userpage(post.userId)">Перейти к пользователю</button>
          </div>
        </div>
      </div>
    </div>

    <modal v-if="isModalOpen" @close="closeModal" :post-id="currentPostId"></modal>
  </div>
</template>

<script>
import modal from '@/components/Comments.vue';
import Menu from '@/components/Menu.vue'
export default {
  components: {
    modal,
    Menu
  },

  data() {
    return {
      posts: [],
      isModalOpen: false,
      currentPostId: null,
    };
  },
  
  mounted() {
   
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(data => (this.posts = data));
      
  },
  methods: {
    openModal(postId) {
      console.log('Opening modal for postId:', postId);
      this.currentPostId = postId;
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
      console.log('Модальное окно закрыто');
      console.log('сшщыовупшщ');
    },
    userpage(userId) {
      this.$router.push({ name: 'user', params: { userId } });
    }
  },
  computed: {
    isDarkMode() {
      return this.$store.state.isDarkMode;
    },
    firstColumn() {
      return this.posts.slice(0, Math.ceil(this.posts.length / 2));
    },
    secondColumn() {
      return this.posts.slice(Math.ceil(this.posts.length / 2));
    },
  },
};
</script>

<style lang="scss" scoped>
  .modal_open {
    // background-attachment: fixed;
    position: fixed;
    // min-width: 98vw;
  }

  .app1{
    display: flex;
    flex-direction: column;
    min-height: fit-content;
    min-width: 98vw;;
   

  }
/* //   .post2 {
//   // position: relative;
//   // transform: rotate(-5%) ;

//   // animation: bendText 4s linear infinite;
// } */

  
  h1{
    display: flex;
    justify-content: center;
    /* // margin: 10px 0; */
    margin-bottom: 5px;
    
  }
  .book{
    display: grid;
    grid-template-columns: 30vw 10px 30vw;
    margin: 80px auto ;
    
    
    @media ( max-width: 788px) {
      grid-template-columns: 55vw 10px;
      animation: bendText 2s 1;
     
      .post-cont1::before {
        width: 56.2vw;
        height: 197.5%;
      }
      .post-cont2 h1{
        display: none;
      }
      .post-cont2{
        border-top: none;
        margin-top: -4rem;
        border-top-left-radius: 0;
        border-top-right-radius: 0;
        border-bottom-left-radius: 90% 25px;
         border-bottom-right-radius: 90% 40px;
      }
      .sq{
        height: 197.25%;
      }
      
    }
  }  
  
  @keyframes bendText {
  0% {
    transform: rotate(-2deg);
  }
  100% {
    transform:  scalex(-1);
  }
}
  .sq{
    background-color: #000000ae;
    position: relative;
    top:1.1rem;
    height: calc(100% - 2.37rem);
  }
  .dark-mode .sq{
    background-color: #ffffffae;
  }
  .post-cont1 {
  position: relative;
  border: 2px solid rgba(0, 0, 0, 0.395);
  border-top-left-radius: 90% 25px;
  border-top-right-radius: 90% 40px;
  border-bottom-left-radius: 90% 25px;
  border-bottom-right-radius: 90% 40px;
  
  padding: 50px 20px;
  box-shadow: -12px 4px 10px  #00000057;
  background-color: #ffffff;
  margin-top: -0.1rem;
  }

  .post-cont1::before {
    content: '';
    position: absolute;
    top: -1.1rem;
    left: -2rem;
    width: 30.6vw;
    height: 100%;
    border: 20px solid rgba(77, 58, 23);
    border-right: 0;
    /* // border-top: 15px;
    // border-top-left-radius: 50% 25px; */
    border-top-right-radius: 50% 37px;
    border-bottom-right-radius: 50% 47px;
    z-index: -1;
  }
  .post-cont2::before {
    content: '';
    position: absolute;
    top: 1.3rem;
    left: -0.1rem;
    width: 30.5vw;
    height: calc(100% - 2.8rem) ; 
    border: 17px solid rgba(77, 58, 23);
    border-left: 0;
    /* // border-top: 20px; */
    border-top-left-radius: 50% 27px;
    border-bottom-left-radius: 50% 38px;
    /* // border-top-right-radius: 30% 20px;
    // transform: rotate(180deg); */
    z-index: -1;
  }
 

 
  .post-cont2{
    margin-top: -23px;
    position: relative;
    border: 2px solid rgba(0, 0, 0, 0.49);
    /* // border-radius:5% 10px 0 20%; */
    border-top-left-radius: 40% 80px;
    border-top-right-radius: 90% 30px;
    border-bottom-left-radius: 90% 40px;
    border-bottom-right-radius: 90% 35px;
    padding: 50px 20px;
    box-shadow: 12px 4px 10px -6px #00000057;
    background-color: #ffffff;
    
  }

  h3{
    text-align: center;
    /* // background-color: rgba(114, 115, 119, 0.19); */
    padding: 20px 0px;
    background:#dfdbdb08 ;
    box-shadow: inset 2px -4px 10px #00000033;
    /* // box-shadow: 10px 0px 10px 0px #424243; */
  }

  p{
    text-align:justify;
    margin: 1rem 2rem;
  }
  .btn{
    display: flex;
    justify-content: center;
    margin: 0.5rem 0;
    gap:1rem
  }
  button{
    /* // display: flex;
    // margin: auto;
    // background-color: #868d9ebf;
    // justify-items: center; */
    margin-bottom:0.5rem ;
    width: 170px;
    border: none;
    border-radius: 40px;
    /* // color: #fff; */
    padding: 10px 5px;
    /* // font-size: 11pt; */
    text-align: match-parent;
    cursor: pointer;
    text-decoration: none;
    /* // margin: 10px; */
    background:#dfdbdb08 ;
    box-shadow: inset 2px -4px 10px #00000033;
  }
  .dark-mode {
    background-color: rgba(23, 23, 23);
    color: white;
  }
  .dark-mode h3 {
    
    box-shadow: inset 2px -4px 10px #ffffff33;
  }
  .dark-mode button {
    box-shadow: inset 2px -4px 10px rgba(255, 255, 255, 0.2);
    color: #ffffff;

  }
  .dark-mode .post-cont1{
    background-color: #57575733;
    box-shadow: -12px 4px 10px  #ffffff57;
  }
  
  .dark-mode .post-cont2{
    background-color: #57575733;
  }
  .dark-mode .post-cont .post {
    border: 2px solid rgba(255, 255, 255, 0.395);
    box-shadow: -12px 4px 10px -6px #ffffff2d;

  }
 
  // .dark-mode .light::before{
  //   border: 0.2rem solid #ffffff0d;
  //   box-shadow: 0px 0px 50px #ffffff00;
  // }
  // .dark-mode .light{
  //   border-right: 0.2rem solid #ffffff0d;
  // }

  // .decor{
  //   display: flex;
  //   position: absolute;
  //   position: fixed;
  //   right: 8vw;
  // }
  // .lamp{
  //   position: relative;
  //   width: 0.7rem;
  //   height: 10rem;
  //   background-image: 
  //       linear-gradient(#000000b3,#000000b3 ),
  //       linear-gradient(#000000b3,#000000b3 ),
  //       linear-gradient(#000000b3,#000000b3 );
  //   background-repeat: no-repeat;
  //   background-size: 
  //       0.15rem 8rem,
  //       0.4rem 0.8rem,
  //       0.7rem 2rem;
  //   background-position:
  //       51.9% 0,
  //       0.14rem 8rem,
  //       0 8.8rem;
  //  z-index: 3;
  // }

  // .lamp::before, .lamp::after {
  //   content: "";
  //   position: absolute;

  // }
  // .lamp::before{
  //   left: -1.65rem;
  //   bottom: -4rem;
  //   width: 4rem;
  //   height: 4rem;
  //   border-radius: 50%;
  //   background:#00000008 ;
  //   box-shadow: inset 2px -2px 10px #00000012;
  //   transition: all 0.75s;
  // }
  // .light,.light::before {
  //   position: absolute;
  // }
  // .light{
  //   top: 10.0rem;
  //   left:0.25rem;
  //   width: 0;
  //   height: 1.5rem;
  //   border-right: 0.2rem solid #0000000d;
  // }

  // .light::before{
  //   content: "";
  //   top: 1.5rem;
  //   left:-0.55rem;
  //   width: 0.9rem;
  //   height: 0.9rem;
  //   border-radius: 50%;
  //   border: 0.2rem solid #0000000d;
  //   /* // box-shadow: 0px 0px 50px #00000012; */
  // }
  // .switch{
  //   position: relative;
  //   width: 4rem;
  //   height: 4rem;
  //   cursor: pointer;
  //   left:2.4rem;
  //   top: 9.9rem;
  //   z-index: 4;
  //   appearance: none;
  // }

  // /* // .post-cont{
  // //   display: flex;
  // //   flex-direction: column;
  // //   // justify-self: center;
  // //   max-width:60vw;
  // //   margin: auto;
  // //   gap:0.5rem;
    
  // // }

  // // .post{
  // //   // border: 2px solid rgba(0, 0, 0, 0.395);
  // //   // box-shadow: -12px 4px 10px -6px #00000057;
  // // } */
 
  // input:checked~.lamp::before{
  //  background-color: #ffffff;
  //  box-shadow: 
  //     0px 2px 10px #ffffffcc,
  //     0px 5px 50px #ffffffcc,
  //     0px 8px 80px #ffffff99,
  //     0px 8px 120px #ffffff99,

  // }

</style>
