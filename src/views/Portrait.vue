<template>
  <div class="home">
    <img src="HfGWortmarke.svg" class="logo" />
    <h2 class="header">talks</h2>
    <h2 class="header hd2">talks</h2>
    <!-- <h2 class="header hd3">talks</h2>-->    
    <div class="hello">
      <div class="strips" :style="{top: strippos+'px'}">
        <div v-for="hour in hours" v-bind:key="hour" class="hourstrip">
          <div class="time">{{hour-1}}:00</div>
          <div class="grid"></div>
        </div>
      </div>
      <div class="talks" :style="{top: strippos+'px'}">
        <div v-for="talk in talks" v-bind:key="talk.hour" class="talkstrip" :style="{height:talk.duration*200+'px', top:(talk.hour*200)+(talk.min*(100/60)/100*200)+'px'}">
          <div class="topic" v-html="talk.topic"></div>
          <div class="speaker">{{talk.speaker}}</div>
        </div>
      </div>
      <div class="arrow"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Portrait',
  props: {
    msg: String
  },
  data: function() {
    return {
      hours: 24,
      strippos: 0,
      talks: [
        {day: "14", hour: 12, min: 0, duration: 0.75, speaker: "Florian Geiselhart", topic: "Secure by Design.<br/> Sicherheit im IoT"},
        {day: "14", hour: 13, min: 0, duration: 0.75, speaker: "Bianca Koch", topic: "Was ist IoT?"},
        {day: "14", hour: 14, min: 0, duration: 0.75, speaker: "Vanessa Stöckel, Jana Seemann", topic: "Rückblick auf das IoT-Studium"},
        {day: "14", hour: 15, min: 0, duration: 0.75, speaker: "IoT BA-Absolventen", topic: "Bachelorarbeiten-Kurzpräsentation"},        
      ]
    };
  },
  mounted() {
    setInterval(() => {
      const vh = Math.max(document.documentElement.clientHeight, window.innerHeight || 0);
      const now = new Date();
      this.strippos = ((vh/2)+20) - (now.getHours() * 200) - (now.getMinutes()*(100/60)/100*200);
    }, 100);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body {
    transform: rotate(90deg);
  }

  .hello {
    font-family: "Roboto";
    overflow: hidden;
    width:100vw;
    height:100vh;
    max-height:100vh;
  }

  .strips, .talks {
    position: absolute;
    left: 20vw;
  }
  
  .hourstrip .grid {
    border: 1px solid #bebebe;
    border-top-style: none;
    border-right-style: solid;
    border-bottom-style: none;
    border-left-style: solid;
    background-image: linear-gradient(to right,#aaaaaa 33%, rgba(255,255,255,0) 0%);
    background-position: bottom;
    background-size: 3px 1px;
    background-repeat: repeat-x;
    height:200px;
    width:60vw;
  }

  .talks {
    margin-left: 166px;
  }

  .talks .speaker {
    font-weight: 400;
    padding:10px;
    padding-right: 20px;
    font-size:24pt;
    display: inline-block;
    position:absolute;
    right:10px;
    color:#aaaaaa;
  }

  .talks .topic {
    font-size: 32pt;
    font-weight: 200;
    padding:10px;
    display: inline-block;
    position:absolute;
    bottom:0;
  }

  .talkstrip {
    position: absolute;
    width: 60vw;
    background-color: rgb(40, 53, 131);
    color:white;
  }

  .hourstrip div {
    display: inline-block;
    vertical-align: top;
  }

  .hourstrip .time {
    margin-right: 15px;
    margin-top:0px;
    width:150px;
    text-align: right;
    font-size: 20pt;
    font-weight: 300;
    color:#ababab;
  }

  .arrow {
    position: absolute;
    top:50%;
    right:12px;
    width: 0; 
    height: 0; 
    border-top: 30px solid transparent;
    border-bottom: 30px solid transparent; 
    border-right:30px solid gray; 
  }

  .logo {
    position: absolute;
    top:60px;
    left:30px;
    width:220px;
  }

  .header {
    font-family: "Roboto";
    font-weight: 200;
    font-size: 18em;
    position: absolute;
    bottom:1vh;
    left:30px;
    color:#f7f7f7;
  }

  .hd2 {
    bottom:1vh;
    left:32px;
    color:#dfdfdf;
    z-index: -9000;
  }

  .hd3 {
    top:64vh;
    left:97px;
    color:#ababab;
    z-index: -9999;
  }

</style>
