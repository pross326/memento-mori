<template>
  <div>
    <v-toolbar
      dark
      rounded
      outlined
      prominent
      id="header"
      height="130px"
      src="https://images.unsplash.com/photo-1502239608882-93b729c6af43?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8NzJ8fHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=500&q=60"
    >
      <v-toolbar-title id="title" class="font-weight-bold ml-2" >Memento Mori</v-toolbar-title>
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

@media only screen and (max-width: 425px) {
  #title {
    font-size: 30px;
    text-align: center;
  }
}

@media only screen and (min-width: 601px) and (max-width: 1024px) {
  #title {
    font-size: 60px;
  }
}

@media only screen and (min-width: 1025px) {
  #title {
    font-size: 80px;
  }
}
</style>>
