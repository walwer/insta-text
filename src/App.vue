<template>
  <div id="main">
    <div class="header">
      <h1 class="title">instaquotes</h1>
    </div>
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
      <div class="form">
        <div contenteditable="true" :style="{'fontFamily':fonts[currentFont].font}" class="input title-prima" cols="10"
             id="main-self" placeholder="Type in here your title..."></div>
        <div contenteditable="true" :style="{'fontFamily':fonts[currentFont].font}" class="input textarea" cols="18"
             id="sub-self" placeholder="Type in here your story..." href="plik.png"></div>
      </div>
      <div class="save btn" @click="makeImage">
        <span>Save as an image</span>
      </div>
    </div>
    <div class="center" v-if="step===1">
      <div class="lds-ellipsis">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
      <p>Saving in progress...</p>
    </div>
    <div class="center" v-if="step===2">
      <p>Done!</p>
      <div class="btn" @click="reload">
        <span>Make another one!</span>
      </div>
    </div>
  </div>
</template>
<script>
    import $ from 'jquery';
    import html2canvas from 'html2canvas';

    export default {
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
        mounted() {
            $('div[contenteditable]').each(function () {
                $(this).html($(this).attr('placeholder'));
                $(this).addClass('placeholder');
                $(this).focus(() => {
                    $(this).removeClass('placeholder');
                    if ($(this).html() === $(this).attr('placeholder')) {
                        $(this).html("");
                        $(this).focus();
                    }
                });
                $(this).blur(() => {
                    if ($(this).html().length === 0) {
                        $(this).html($(this).attr('placeholder'));
                        $(this).addClass('placeholder');
                    }
                });

            });
        },
        methods: {
            reload: function () {
                window.location.reload();
            },
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

                        Canvas2Image.saveAsPNG(canvas, canvas.width, canvas.height, 'story_image');
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

    .header {
      width: 100vw;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;

      .title {
        padding: 30px;
        margin: 0;
        font-size: 20px;

        color: #333;
      }

    }

    .center {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 30px;

      .form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        text-align: left;
        border: 1px dashed #CCC;
        border-radius: 10px;
        overflow: hidden;
        width: 270px;
        height: 480px;
        box-sizing: border-box;
        padding: 25px;

        .input {
          outline: none;
          margin: 0;
          padding: 0;
          border: 0;
          /*resize: vertical;*/
          padding: 5px;
          /*height: 100px;*/
          text-align: left;
          font-family: "Times New Roman";
          font-size: 20px;
          resize: none;
          overflow: hidden;
          max-width: 100%;
          width: 100%;

          &.placeholder {
            opacity: 0.6;
          }

          &.title-prima {
            font-size: 35px;
          }

          &.textarea {
            font-style: italic;
            box-sizing: border-box;

          }
        }
      }

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
