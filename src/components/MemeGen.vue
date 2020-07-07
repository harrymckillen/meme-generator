<template>
  <div class="memes">
    <v-stage class="stage" ref="stage" :config="stageSize">
      <v-layer ref="layer">
        <v-image :config="{
          image: image,
          width: stageSize.width,
          height: stageSize.height
        }"/>
        <v-text ref="text" :config="{
          fontFamily: typeface,
          fontSize: 36,
          text: memeText.toUpperCase(),
          fill: 'white',
          stroke: 'black',
          strokeWidth: 1,
          width: stageSize.width-10,
          height: stageSize.height-10,
          align: 'center',
          verticalAlign: 'bottom'
        }" />
      </v-layer>
    </v-stage>
    <div class="flex">
      <div class="fortypc">
        <textarea v-model="memeText"></textarea>
      </div>
      <div class="sixtypc">
        <div class="font-selector">
          <div class="fiftypc">
            <a :class="activeClass(fonts.slot1)"
              :style="{ fontFamily: fonts.slot1 }"
              @click="switchFont(fonts.slot1)">
                {{fonts.slot1}}
            </a>
          </div>
          <div class="fiftypc">
            <a :class="activeClass(fonts.slot2)"
              :style="{ fontFamily: fonts.slot2 }"
              @click="switchFont(fonts.slot2)">
                {{fonts.slot2}}
            </a>
          </div>
          <div class="fiftypc">
            <a :class="activeClass(fonts.slot3)"
              :style="{ fontFamily: fonts.slot3 }"
              @click="switchFont(fonts.slot3)">
                {{fonts.slot3}}
            </a>
          </div>
          <div class="fiftypc">
            <a :class="activeClass(fonts.slot4)"
              :style="{ fontFamily: fonts.slot4 }"
              @click="switchFont(fonts.slot4)">
              {{fonts.slot4}}
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemeGen',
  data: function(){
    return {
      memeText: 'Your meme text here',
      typeface: 'Anton',
      stageSize: {
        width: 720,
        height: 400
      },
      image: null,
      fonts: {
        slot1: 'Anton',
        slot2: 'Bangers',
        slot3: 'Fredoka One',
        slot4: 'Zilla Slab'
      }
    }
  },
  created: function(){
    const image = new window.Image();
    image.src = '/images/wonka.jpg';
    console.log(image);
    image.onload = () => {
      // set image only when it is loaded
      this.image = image;
    };
  },
  methods: {
    switchFont(value){
      this.typeface = value;
    },
    activeClass(value){
      let activeClassName = '';

      if(this.typeface === value){
        activeClassName = 'active';
      }

      return activeClassName;
    }
  }
}
</script>

<style scoped>
  .flex, .font-selector {
    display: flex;
    align-content: space-between;
  }
  .font-selector{
    min-height: 100px;
    margin: 1em 0;
    flex-wrap: wrap;
  }
  .font-selector a {
    display: block;
    text-align: center;
    cursor: pointer;
    font-size: 28px;
    line-height: 50px;
    margin: 0.1em 0.5em;
  }
  .font-selector a.active, .font-selector a:hover  {
    border: 2px solid #fff;
    line-height: 46px;
  }
  .fortypc{
    width: 40%;
  }
  .fiftypc{
    width: 50%;
  }
  .sixtypc{
    width: 60%;
  }
  .stage {
    margin:1em 0 2em 0;
  }
  .memes {
    width: 720px;
    display: block;
    margin: 0 auto;
  }
  textarea {
    margin: 1em 0;
    display: block;
    width: 95%;
    height: 100px;
  }
</style>
