<template>
  <div class="form">
    <div contenteditable="true"  :style="{'fontFamily':fonts[currentFont].font}" class="input title-prima" cols="10"
         id="main-self" placeholder="Type in here your title..."></div>
    <div contenteditable="true" :style="{'fontFamily':fonts[currentFont].font}" class="input textarea" cols="18"
         id="sub-self" placeholder="Type in here your story..." href="plik.png"></div>
  </div>
</template>

<script>
  import $ from 'jquery';

    export default {
        name: "Form",
        props: ['fonts','currentFont'],
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
        }
    }
</script>

<style scoped lang="scss">
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
</style>
