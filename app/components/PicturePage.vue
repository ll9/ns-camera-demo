<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <ScrollView>
        <StackLayout id="stack">
            <Button text="take a picture" @tap="takePicture" />
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
