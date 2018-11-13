<template>
    <Page>
        <ActionBar title="Welcome to NativeScript-Vue!"/>
        <GridLayout columns="*, *" rows="200, 200">
            <Button text="Karte" col="0" row="0" />
            <Button text="Erfassen" @tap="nav" col="1" row="0" />
            <Button text="Bestand" col="0" row="1" />
            <Button text="Einstellungen" col="1" row="1" />
        </GridLayout>
    </Page>
</template>

<script>
import PicturePage from './PicturePage';

  export default {
    data() {
      return {
        msg: 'Hello World!'
      }
    },
    methods: {
        nav() {
            this.$navigateTo(PicturePage);
        }
    }
  }
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
