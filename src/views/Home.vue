<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button></ion-back-button>
          <ion-menu-button></ion-menu-button>
        </ion-buttons>
        <ion-title>TEST CANVAS PAGE</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content id="main">
      <div v-pre id="editor2">
        <div id="rowbuild2">
          <canvas id="test-canvas"></canvas>
          <canvas id="test-canvas2"></canvas>
          <button id="top-button">TOP</button>

          <div id="bottom-menu">
            <button id="bottom-button">
              CLICK BUTTON TO GENERATE BUTTON
            </button>
          </div>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<style lang="css" scoped>
  #editor2 {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background-color: red;
  }

  #rowbuild2 {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background-color: yellow;
  }

  #bottom-menu {
    svg {
      width: 20px;
      height: 20px;
    }
  }
</style>

<script>
  import {
    IonPage, IonContent, IonHeader, IonToolbar, IonTitle, IonButtons, IonMenuButton,
  } from '@ionic/vue';
  import $ from 'jquery';
  // export for others scripts to use
  window.$ = $;

  export default {
    name: 'TgCanvasTest',

    components: {
      IonPage,
      IonContent,
      IonHeader,
      IonToolbar,
      IonTitle,
      IonButtons,
      IonMenuButton,
    },

    data: function () {
      return {}
    },

    setup() {

    },

    created() {

    },

    mounted() {
      let $canvasTest   = $('#test-canvas'),
          $canvasTest2  = $('#test-canvas2'),
          $topButton    = $('#top-button'),
          $testInput    = $('#test-input'),
          $bottomButton = $('#bottom-button'),
          $bottomMenu   = $('#bottom-menu'),
          height        = $(window).innerHeight() - 50 - 50 - 40 - 56, //ionic header/topbutton/input/bottom button
          width         = $(window).innerWidth();

      $bottomButton.on('click', function () {
        if ($testInput.length !== 0) {
          return;
        }

        let top = $('#editor2').height() - 90;
        //USING TOP INSTEAD OF BOTTOM CAUSE THE ISSUE/PLUS DYNAMICALLY CREATING THE ELEMENT
        $testInput = $('<input type="text" id="test-input" value="TEST" style="height: 40px; left: 0; right: 0; position: absolute; width: 100%; top: ' + top + 'px;"/>');
        $bottomMenu.parent().append($testInput);
        $testInput = $('#test-input');
      });

      $topButton.css({
        position: 'absolute',
        top: 0,
        left: 0,
        right: 0,
        height: '50px',
        width: '100%'
      });

      $testInput.css({
        position: 'absolute',
        bottom: '50px',
        left: 0,
        right: 0,
        height: '40px',
        width: '100%',
      })
      $bottomMenu.css({
        position: 'absolute',
        bottom: 0,
        left: 0,
        right: 0,
        width: '100%',
        height: '50px',
      })
      $bottomButton.css({
        // position: 'absolute',
        // bottom: 0,
        // left: 0,
        // right: 0,
        width: '100%',
        height: '50px',
      })

      console.log('height:', height, 'width:', width);
      $canvasTest
          .css({
            position: 'absolute',
            top: '50px',
          })
          .attr('width', width)
          .attr('height', height);

      $canvasTest2
          .attr('width', width)
          .attr('height', height)
          .css({
            position: 'absolute',
            top: '50px',
          })

      let cWidth  = width,// $canvasTest.width(),
          cHeight = height;// $canvasTest.height();
      console.log('W/D:', cWidth, cHeight);

      var c   = document.getElementById("test-canvas");
      var ctx = c.getContext("2d");

      var c2   = document.getElementById("test-canvas2");
      var ctx2 = c2.getContext("2d");

      setTimeout(function () {
        ctx.fillStyle = 'green';
        ctx.fillRect(0, 0, cWidth, cHeight);
        ctx2.fillStyle = 'blue';
        ctx2.fillRect(10, 10, (cWidth - 20), (cHeight - 20));
      }, 1000);
    },

    methods: {}
  }
</script>
