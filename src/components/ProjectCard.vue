<template>
  <div>
    <section v-if="!editing" class="project">
      <div class="image"></div>
      <div class="textContent">
        <div class="header-box">
          <h4 class="title">{{ name }}</h4>
          <div class="btns">
            <span @click="edit"> <i class="fas fa-times"></i></span>
            <span @click="remove"> <i class="fas fa-pencil-alt"></i></span>
          </div>
        </div>
        <p class="text">{{ description }}</p>
      </div>
    </section>
    <section v-else class="project">
      <input type="text" v-model="name">
      <input type="text" v-model="description">
      <button @click="save">Save</button>
      <button @click="remove">Delete</button>
    </section>
  </div>
</template>

<style lang="scss">
.project {
  display: flex;
  max-height: 80px;
  margin: 30px 0;

  .image {
    background: url('/assets/img-ciudad.jpg');
    width: 91px;
    height: 91px;
    background-size: cover;
    margin-right: 20px;
    background-repeat: no-repeat;
    background-position: center center;
  }

  .textContent {
    .title {
      margin: 0;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: flex-start;
    }

    .header-box{
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      margin: 5px 0;
      .btns {
        span{
          width: 20px;
          width: 20px;
          margin: 0 5px;
        }
      }
    }


    .text {
      margin: 0;
    }
  }
}

</style>

<script>
export default {
  name: "ProjectCard",
  props: ["name", "description", "id", "onRemove"],
  data: () => ({
      editing: false,
  }),
  methods: {
    remove: function() {
      this.onRemove(this.id);
    },
    edit: function() {
        this.editing = true;
    },
    save: function() {
        this.editing = false;
    }
    
  }
};
</script>
