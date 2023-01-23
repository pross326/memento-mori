<template>
  <div>
    <v-toolbar
      dark
      rounded
      outlined
      prominent
      id="header"
      height="170px"
      src="https://images.unsplash.com/photo-1502239608882-93b729c6af43?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8NzJ8fHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60"
    >
      <v-toolbar-title id="title" style="font-size: 100px;" class="font-weight-bold ml-2" >Memento Mori</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
  </div>
</template>

<script>
export default {
  name: "siteHeader",
};
</script>

<style>
#title {
  font: 'Merriweather', serif;
}
#header{
  background-position: center;
  background-size: cover;
}
</style>
