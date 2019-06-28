<template>
  <div id="main">
    <Header/>
    <div class="center" v-if="step===0">
      <div class="options">
        <h3>options</h3>
        <div class="option-group">
          <label for="font-selection">Font</label>
          <div class="font-holder" id="font-selection">
            <div class="font-box" v-if="fontModal">
              <p v-for="font in fonts" :key="font.id" @click="selectFont(font.id)" :style="{'fontFamily':font.font}">
                {{font.name}}</p>
            </div>
            <p class="current-font" @click="fontModal=true" :style="{'fontFamily':fonts[currentFont].font}">
              {{fonts[currentFont].name}}</p>
          </div>
        </div>
      </div>
      <Form :fonts="fonts" :current-font="currentFont"/>
      <div class="save btn" @click="makeImage">
        <span>Save as an image</span>
      </div>
    </div>
    <_step1 v-if="step===1"/>
    <_step2 v-if="step===2"/>
  </div>
</template>
<script>
    import html2canvas from 'html2canvas';
    import $ from 'jquery';

    import Header from './components/Header.vue';
    import Form from './components/Form.vue';
    import _step2 from "./views/_step2";
    import _step1 from "./views/_step1";

    export default {
        components: {
            _step1,
            _step2,
            Header,
            Form
        },
        data() {
            return {
                fonts: [
                    {
                        id: 0,
                        font: 'Times New Roman',
                        name: 'Classic'
                    },
                    {
                        id: 1,
                        font: 'Playfair Display',
                        name: 'Business'
                    },
                    {
                        id: 2,
                        font: 'Arapey',
                        name: 'Wavy'
                    },
                    {
                        id: 3,
                        font: 'Cormorant',
                        name: 'Linen'
                    }
                ],
                currentFont: 0,
                step: 0,
                fontModal: false
            }
        },
        methods: {
            selectFont: function (id) {
                this.currentFont = id;
                this.fontModal = false;
            },
            makeImage: function () {

                let element = $('.form').get(0);
                $(element).css('border', 'none');
                $(element).css('position', 'fixed');
                $(element).css('top', 0);
                $(element).css('left', 0);
                $(element).css('box-sizing', 'border-box');
                html2canvas(element)
                    .then((canvas) => {
                        $(element).remove();
                        Canvas2Image.saveAsPNG(canvas, canvas.width, canvas.height, 'story');
                    });
                this.step = 1;
                setTimeout(() => {
                    this.step = 2;
                }, 2000);
            }
        }
    }
</script>
<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Mali:300,400,500&display=swap');

  body {
    margin: 0;
    font-family: "Mali", sans-serif;
  }

  #main {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;

    .center {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 30px;
      margin-top: 30px;


      .btn {
        padding: 10px 20px;
        margin-top: 20px;
        border: 2px solid #333;
        color: #333;
        text-transform: uppercase;
        font-weight: 700;
        transition: .2s ease;
        cursor: pointer;

        &:hover {
          background: #333;
          color: #FFF;

        }
      }

      .options {
        padding: 20px;

        h3 {
          color: #666;
          font-weight: 400;
        }

        .option-group {
          display: grid;
          grid-template-columns: 1fr 1fr;
          grid-gap: 20px;
          width: min-content;
          border-bottom: 1px dashed #EEE;
          padding: 10px;

          .font-holder {
            position: relative;
            width: 100px;
            font-size: 20px;

            p {
              margin: 0;
            }

            .font-box {
              position: absolute;
              padding: 10px;
              background: #FFF;
              border: 1px dashed #CCC;

              p {
                padding: 5px;
              }
            }
          }

          .h3 {
            color: #555;
          }

        }

      }
    }
  }

</style>
