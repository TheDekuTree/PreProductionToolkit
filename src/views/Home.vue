<template>
  <div class="home">
    <div class="n-header-bg">
      <h1 class="mainTitle">Pre-Production</h1>
      <h1 class="subTitle">Toolkit</h1>
    </div>
    <div style="" class="offsetMain ui four column doubling stackable">
      <div class="ui raised very padded text container segment">
        <h1 class="ui">Production Schedule</h1>
        <p>Manage your production schedule using our flexible and easy to use tools. When it comes time to make a shooting schedule, gone are the days of copying and pasting from a spreadsheet or table. Pre-Production toolkit will automatically generate a shooting schedule from your existing production schedule.</p>
      </div>
      <div class="ui raised very padded text container segment">
        <h1 class="ui">Shooting Schedule</h1>
        <p>The shooting schedule is a very important part of the production, it keeps you organized while on set. Pre-Production Toolkit auto generates a responsive, detailed and flexible shooting schedule for you.</p>
      </div>
      <div class="ui raised very padded text container segment">
        <h1 class="ui">Ready?</h1>
        <p>Try Pre-Production Toolkit today! It's 100% free and open source, garenteed to make pre-production easier than ever!</p>
        <router-link class="ui google plus button primary" to="/generate">Let's Go!</router-link>
      </div>
    </div>
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
$(window).scroll(function() {
  $(".header").css("opacity", 1 - $(window).scrollTop() / 500);
});

export default {
  name: "home",
  components: {
    //HelloWorld
  }
};
</script>
