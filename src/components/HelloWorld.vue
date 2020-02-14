<template>
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
        {day: "14", hour: 12, min: 30, duration: 0.75, speaker: "Bianca Koch", topic: "Was ist IoT?"},
        {day: "14", hour: 14, min: 0, duration: 0.75, speaker: "Prof. Hartmut Bohnacker", topic: "Creative Coding"},
        {day: "14", hour: 15, min: 30, duration: 0.75, speaker: "Ludwig Kannicht", topic: "Das Neue zähmen.<br/> Wie Gestalter arbeiten."},
        {day: "14", hour: 17, min: 0, duration: 0.75, speaker: "Florian Geiselhart", topic: "Secure by Design.<br/> Sicherheit im IoT"},
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
  .hello {
    font-family: "Roboto";
    overflow: hidden;
    width:100vw;
    height:100vh;
    max-height:100vh;
  }

  .strips, .talks {
    position: absolute;
    left: 40vw;
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
    width:43vw;
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
    width: 43vw;
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
    right:120px;
    width: 0; 
    height: 0; 
    border-top: 30px solid transparent;
    border-bottom: 30px solid transparent; 
    border-right:30px solid gray; 
  }

</style>
