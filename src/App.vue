<template>
  <div id="main">
    <div class="header">
      <h1 class="title">yourQuotes</h1>
    </div>
    <div class="center">
      <div class="form">
        <textarea class="input title-prima" placeholder="Type in here your title..."></textarea>
        <textarea class="input textarea" contenteditable="true" placeholder="Type in here your story..."></textarea>
      </div>
      <div class="save btn">
        <span>Save as an image</span>
      </div>
    </div>
  </div>
</template>
<script>
  import $ from 'jquery';
  export default {
      mounted() {
          function autoresize(textarea) {
              textarea.style.height = '0px';     //Reset height, so that it not only grows but also shrinks
              textarea.style.height = (textarea.scrollHeight+10) + 'px';    //Set new height
          }
          $('textarea').keyup(function () {
              autoresize(this);
          });
          $(function () {
              $("textarea").each(function () {
                  this.style.height = (this.scrollHeight+10)+'px';
              });
          });
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
      background: #FFF;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      display: flex;
      flex-direction: column;

      .title {
        padding: 10px;
        margin: 0;
        color: #444;
      }

    }
    .center {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 50px;
      .form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        text-align: left;
        border: 1px dashed #CCC;
        padding: 50px;
        border-radius: 10px;
        .input {
          outline: none;
          margin: 0;
          padding: 0;
          border: 0;
          resize: vertical;
          padding: 10px;
          text-align: left;
          font-family: "Times New Roman";
          font-size: 25px;
          resize: none;
          overflow: hidden;
          &.title-prima {
            font-size: 40px;
          }
          &.textarea {
            font-style: italic;
            width: 100%;
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
    }
  }

</style>
