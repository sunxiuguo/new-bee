<template>
    <div id="section">
       <section class="hero bd-rainbow-newbee">
    <div class="hero-body">
      <div class="container">
        <div class="columns is-vcentered">
          <div class="column">
            <p class="title">
              开发者成长的开源社区
            </p>

            <br>
            <small class="subtitle  content h6">
              <div id="typeWriter" style="float:left"></div>
              <strong id="typeWriter" style="float:left">New Bee</strong>
            </small>
          </div>
          <div class="column is-narrow">
             

          </div>
        </div>
      </div>
    </div>

    <div class="hero-foot">
      <div class="container">
        <nav class="tabs is-boxed">
          <ul>
            <li  v-for="tag in tagList" v-bind:key="tag" :type="tag">
              <a>{{tag}}</a>
            </li>
             

          </ul>
        </nav>
      </div>
    </div>

  </section>

  <div id="modal-ter" class="modal">
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Modal title</p>
        <button class="delete close-modal" data-target="modal-ter"></button>
      </header>
      <section class="modal-card-body">
        <div class="content">a\na\n</div>
      </section>

    </div>
  </div>


  <div class="container" id="index-type">
    <div class="bd-snippet-preview ">
      <a class="button is-danger is-focused" @click="sortBy('commendCount')">热门</a>
      <a class="button is-warning is-focused" @click="sortBy('createTime')">最新</a>
      <a class="button is-info is-focused" @click="sortBy('starCount')">收藏</a>
      <a class="button is-primary is-focused" @click="sortBy('commentCount')">评论</a>
    </div>
    <hr>
  </div>
    </div>
</template>


<script>
export default {
  name: "Section",
  props: { tagList: Array },
  data() {
    return {};
  },
  mounted() {
    let self = this;
    $("nav.tabs")
      .find("li")
      .click(function() {
        if (!$(this).hasClass("is-active")) {
          $("nav.tabs")
            .find("li")
            .each(function(k, v) {
              $(v).removeClass("is-active");
            });
          $(this).addClass("is-active");
          self.$emit("tagEvent", $(this).attr("type"));
          //todo:应该减少dom移出操作
          $("#index-main").hide();
          newBee("#index-type").animation(500, function() {
            $("#index-main").show();
          });
        }
      });
    var typeWriterDom = document.getElementById("typeWriter");

    var typewriter = new Typewriter(typeWriterDom, {
      loop: false,
      deleteSpeed: 500
    });

    typewriter
      .typeString("-")
      .pauseFor(2500)
      .typeString(" 世界因我而")
      .pauseFor(2000)
      .deleteChars(2)
      .pauseFor(1000)
      .typeString("你我而")
      .pauseFor(1000)
      .start();
  },
  destroyed() {},
  methods: {
    sortBy(type) {
      this.$emit("buttonEvent", type);
    }
  }
};
</script>
