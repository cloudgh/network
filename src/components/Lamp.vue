  <template>
    <div class="decor" :class="{ 'dark_mode': isDarkMode }">
      <input type="checkbox" class="switch" v-model="isDarkMode">
      <div class="lamp">
        <div class="light"></div>
      </div>
    </div>
  </template>
  
  <script>
    export default {
      name: "Lamp",
      computed: {
        isDarkMode: {
          get() {
            return this.$store.state.isDarkMode;
          },
          set(value) {
            this.$store.commit("updateDarkMode", value);
          },
        },
      },
    };
  </script>
  
  
<style>
.decor{
    display: flex;
    position: absolute;
    position: fixed;
    right: 8vw;
  }
  .lamp{
    position: relative;
    width: 0.7rem;
    height: 10rem;
    background-image: 
        linear-gradient(#000000b3,#000000b3 ),
        linear-gradient(#000000b3,#000000b3 ),
        linear-gradient(#000000b3,#000000b3 );
    background-repeat: no-repeat;
    background-size: 
        0.15rem 8rem,
        0.4rem 0.8rem,
        0.7rem 2rem;
    background-position:
        51.9% 0,
        0.14rem 8rem,
        0 8.8rem;
   z-index: 3;
  }

  .lamp::before, .lamp::after {
    content: "";
    position: absolute;

  }
  .lamp::before{
    left: -1.65rem;
    bottom: -4rem;
    width: 4rem;
    height: 4rem;
    border-radius: 50%;
    background:#00000008 ;
    box-shadow: inset 2px -2px 10px #00000012;
    transition: all 0.75s;
  }
  .light,.light::before {
    position: absolute;
  }
  .light{
    top: 10.0rem;
    left:0.25rem;
    width: 0;
    height: 1.5rem;
    border-right: 0.2rem solid #0000000d;
  }

  .light::before{
    content: "";
    top: 1.5rem;
    left:-0.55rem;
    width: 0.9rem;
    height: 0.9rem;
    border-radius: 50%;
    border: 0.2rem solid #0000000d;
    /* // box-shadow: 0px 0px 50px #00000012; */
  }
  .switch{
    position: relative;
    width: 4rem;
    height: 4rem;
    cursor: pointer;
    left:2.4rem;
    top: 9.9rem;
    z-index: 4;
    appearance: none;
  }


 
  input:checked~.lamp::before{
   background-color: #ffffff;
   box-shadow: 
      0px 2px 10px #ffffffcc,
      0px 5px 50px #ffffffcc,
      0px 8px 80px #ffffff99,
      0px 8px 120px #ffffff99;
    z-index: 2;

  }
  .dark_mode .light::before{
    border: 0.2rem solid #ffffff0d;
    box-shadow: 0px 0px 50px #ffffff00;
  }
  .dark_mode .light{
    border-right: 0.2rem solid #ffffff0d;
  }
</style>