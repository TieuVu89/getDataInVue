<template>
  <div class="hello">
    <table border="1px;" style="border-collapse: collapse">
      <tr>
        <td>albumId</td>
        <td>id</td>
        <td>thumbnailUrl</td>
        <td>title</td>
        <td>url</td>
      </tr>
      <tr v-for="item in dataPhotoPromise" :key="item.id">
        <td>{{ item.albumId }}</td>
        <td>{{ item.id }}</td>
        <td>{{ item.thumbnailUrl }}</td>
        <td>{{ item.title }}</td>
        <td>{{ item.url }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
// import Vue from "vue";

export default {
  name: "HelloWorld",
  data() {
    return {
      dataPhotoPromise: undefined,
      dataCommentPromise: undefined,
      dataTodoPromise: undefined,
      dataPhotoCallback: undefined,
      dataCommentCallback: undefined,
      dataTodoCallback: undefined,
      dataPhotoAsyncAwait: undefined,
      dataCommentAsyncAwait: undefined,
      dataTodoAsyncAwait: undefined,
    };
  },
  async mounted() {
    var t0 = performance.now();
    this.callapi();
    var t1 = performance.now();
    console.log("time run with async/ await : " + (t1 - t0) + " miliseconds");
    var t2 = performance.now();
    this.FetchApi();
    var t3 = performance.now();
    console.log("time run with promise : " + (t3 - t2) + " miliseconds");
    // var t4 = performance.now();
    // this.getdataPhoto(this.getdataComment(this.getdataTodo()));
    // var t5 = performance.now();
    // console.log("time run with callback" + (t5 - t4) + "miliseconds");
  },
  methods: {
    //promise
    FetchApi() {
      fetch("https://jsonplaceholder.typicode.com/photos")
        .then((resp) => {
          return resp.json();
        })
        .then((data) => {
          this.dataPhotoPromise = data;
          fetch("https://jsonplaceholder.typicode.com/comments")
            .then((resp) => {
              return resp.json();
            })
            .then((data) => {
              this.dataCommentPromise = data;
              fetch("https://jsonplaceholder.typicode.com/todos")
                .then((resp) => {
                  return resp.json();
                })
                .then((data) => {
                  this.dataTodoPromise = data;
                })
                .catch((err) => {
                  console.log("rejected", err);
                });
            })
            .catch((err) => {
              console.log("rejected", err);
            });
        })
        .catch((err) => {
          console.log("rejected", err);
        });
    },
    //callback
    // getdataComment(callback) {
    //   fetch("https://jsonplaceholder.typicode.com/comments")
    //     .then((resp) => {
    //       return resp.json();
    //     })
    //     .then((data) => {
    //       this.dataCommentCallback = data;
    //     })
    //     .catch((err) => {
    //       console.log("rejected", err);
    //     });
    //   callback();
    // },
    // getdataPhoto(callback) {
    //   fetch("https://jsonplaceholder.typicode.com/photos")
    //     .then((resp) => {
    //       return resp.json();
    //     })
    //     .then((data) => {
    //       this.dataPhotoCallback = data;
    //     })
    //     .catch((err) => {
    //       console.log("rejected", err);
    //     });
    //   callback();
    // },
    // getdataTodo() {
    //   fetch("https://jsonplaceholder.typicode.com/todos")
    //     .then((resp) => {
    //       return resp.json();
    //     })
    //     .then((data) => {
    //       this.dataTodoCallback = data;
    //     })
    //     .catch((err) => {
    //       console.log("rejected", err);
    //     });
    // },
    //async/await
    async callapi() {
      try {
        this.dataPhotoAsyncAwait = await fetch(
          "https://jsonplaceholder.typicode.com/photos"
        );
        this.dataCommentAsyncAwait = await fetch(
          "https://jsonplaceholder.typicode.com/comments"
        );
        this.dataTodoAsyncAwait = await fetch(
          "https://jsonplaceholder.typicode.com/todos"
        );
        // console.log(
        //   this.dataPhotoAsyncAwait,
        //   this.dataCommentAsyncAwait,
        //   this.dataTodoAsyncAwait,
        //   "async/await"
        // );
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
