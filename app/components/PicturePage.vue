<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <ScrollView>
        <StackLayout id="stack">
            <Button text="take a picture" @tap="takePicture" />
            <Button text="from Gallery" @tap="getFromGallery" />
        </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
import * as camera from "nativescript-camera";
require("nativescript-dom");
import * as imageModule from "tns-core-modules/ui/image";
import {
  ImageSource,
  fromFile,
  fromResource,
  fromBase64
} from "tns-core-modules/image-source";
import * as imagepicker from "nativescript-imagepicker";

let context = imagepicker.create({
  mode: "single" // use "multiple" for multiple selection
});

export default {
  data() {
    return {
      images: []
    };
  },
  computed: {
    any() {}
  },
  methods: {
    takePicture() {
      camera
        .requestPermissions()
        .then(() => {
          console.log("granted");
          camera
            .takePicture(/*{width: 200, height: 200, keepAspectRatio: false, saveToGallery: false}*/)
            .then(imageAsset => {
              let stack = getElementById("stack");
              console.log(stack);
              var image = new imageModule.Image();
              image.src = imageAsset;

              let source = new ImageSource();
              source.fromAsset(imageAsset).then(source => {
                const base64image = source.toBase64String("jpg", 60);
                this.images.push(base64image);
              });
              stack.addChild(image);
            });
        })
        .catch(err => console.log(err));
    },
    getFromGallery() {
      let stack = getElementById("stack");

      context
        .authorize()
        .then(function() {
          return context.present();
        })
        .then(function(selection) {
          selection.forEach(function(selected) {
            // process the selected image
            console.log(selected);
            var image = new imageModule.Image();
            image.src = selected;
            stack.addChild(image);
          });
        })
        .catch(function(e) {
          // process error
        });
    }
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
</style>
