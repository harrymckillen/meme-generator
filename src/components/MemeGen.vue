<template>
  <div class="memes">
    <div v-if="image">
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
          <div class="flex font-selector">
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
      <div class="full reset">
        <a @click="removeImage()">Reset</a>
      </div>
    </div>
    <div v-else class="file-upload">
      <label for="memeUpload">Choose a picture: </label>
      <input type="file" @change="memeUpload"
        id="memeUpload" name="memeUpload"
        accept="image/png, image/jpeg">
    </div>
  </div>
</template>

<script>
export default {
  name: 'MemeGen',
  data: function(){
    return {
      memeText: 'Your meme text here',
      typeface: 'Akbar',
      stageSize: {
        width: 720,
        height: 400
      },
      image: null,
      fonts: {
        slot1: 'Akbar',
        slot2: 'Anton',
        slot3: 'Bangers',
        slot4: 'Zilla Slab'
      }
    }
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
    },
    memeUpload(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length) {
        return
      }
      this.createImage(files[0]);
    },
    createImage(file) {
      let reader = new FileReader();
      let imageEl = new window.Image();

      reader.onload = () => {
        imageEl.src = reader.result;
        imageEl.onload = () => {
          if(imageEl.width < this.stageSize.width || imageEl.height < this.stageSize.height){
            this.stageSize.width = imageEl.width;
            this.stageSize.height = imageEl.height;
          } else if(imageEl.width > this.stageSize.width || imageEl.height > this.stageSize.height) {
            var ratio;
            if(imageEl.width > imageEl.height){
              ratio = (imageEl.height/imageEl.width).toFixed(2);
              this.stageSize.height = (this.stageSize.width*ratio).toFixed(0);
            }else {
              ratio = (imageEl.width/imageEl.height).toFixed(2);
              this.stageSize.height = (this.stageSize.width/ratio).toFixed(0);
            }
          }
        };

        this.image = imageEl;
      }
      reader.readAsDataURL(file);
    },
    removeImage: function () {
      this.image = null;
    }
  }
}
</script>

<style>
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
  .stage {
    margin: 1em 0 2em 0;
  }
  .stage div {
    margin: 0 auto;
  }
  .memes, .file-upload {
    width: 720px;
    display: block;
    margin: 0 auto;
  }
  .file-upload{
    text-align: center;
  }
  .reset {
    text-align: center;
  }
  .reset a {
    padding: 0.5em 1em;
    cursor: pointer;
    background: #fff;
    color: #333;
    /* border: 2px solid #fff; */
    font-size: 1.25rem;
  }
  textarea {
    margin: 1em 0;
    display: block;
    width: 95%;
    height: 100px;
    resize: none;
  }
</style>
