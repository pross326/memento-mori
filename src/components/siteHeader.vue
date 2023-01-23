<template>
  <div>
    <v-toolbar
      dark
      rounded
      outlined
      prominent
      id="header"
      height="170px"
      src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTY4StVrn06Uh54Z8m6GllhrhVfX3TLtet3VotxCs3tWOoQamg812sDltbjPZaJB9BT5Zo&usqp=CAU"
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
  background-position: center bottom;
  background-size: contain;
}
</style>
