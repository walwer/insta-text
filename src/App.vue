<template>
  <div id="main">
    <div class="header">
      <h1 class="title">instaquotes</h1>
    </div>
    <div class="center">
      <div class="options">
        <h3>options</h3>
        <div class="option-group">
          <label for="font-selection">Font</label>
          <select name="font-selection" id="font-selection" v-model="currentFont">
            <option v-for="font in fonts" :key="font" :value="font">{{font}}</option>
          </select>
        </div>
      </div>
      <div class="form">
        <div contenteditable="true" :style="{'fontFamily':currentFont}" class="input title-prima" cols="10" id="main-self" placeholder="Type in here your title..."></div>
        <div contenteditable="true" :style="{'fontFamily':currentFont}" class="input textarea" cols="18" id="sub-self" placeholder="Type in here your story..." href="plik.png"></div>
      </div>
      <div class="save btn" @click="makeImage">
        <span>Save as an image</span>
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
              fonts: ['Times New Roman','Arial','Tahoma'],
              currentFont: 'Times New Roman'
          }
      },
      mounted() {
          // function autoresize(textarea) {
          //     textarea.style.height = '0px';     //Reset height, so that it not only grows but also shrinks
          //     textarea.style.height = (textarea.scrollHeight+10) + 'px';    //Set new height
          // }
          // $('textarea').keyup(function () {
          //     autoresize(this);
          // });
          // $(function () {
          //     $("textarea").each(function () {
          //         this.style.height = (this.scrollHeight+10)+'px';
          //     });
          // });
          $('div[contenteditable]').each(function(){
              $(this).html($(this).attr('placeholder'));
              $(this).addClass('placeholder');
              $(this).focus(()=>{
                  $(this).removeClass('placeholder');
                  if($(this).html() === $(this).attr('placeholder')){
                      $(this).html("");
                      $(this).focus();
                  }
              });
              $(this).blur(()=>{
                  if($(this).html().length === 0){
                      $(this).html($(this).attr('placeholder'));
                      $(this).addClass('placeholder');
                  }
              });

          });
      },
      methods: {
          makeImage: function(){

            let element = $('.form').get(0);
            // $(element).css('transform','scale(2)');
            $(element).css('border','none');

            html2canvas(element)
                .then((canvas)=>{
                    $(element).remove();
                    // let image = Canvas2Image.convertToPNG(canvas,canvas.width,canvas.height);
                    // $('.center').append(image);
                    Canvas2Image.saveAsPNG(canvas,canvas.width,canvas.height,'story_image');
                });
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
        .option-group {
          display: grid;
          grid-template-columns: 1fr 1fr;
          grid-gap: 10px;
          width: min-content;
          .h3 {
            color: #555;
          }
          select {
            padding: 10px 20px;
            font-size: 15px;
            outline: none;
            border: none;
            background: #FFF;
          }
        }

      }
    }
  }

</style>
