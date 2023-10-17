<template>
  <div>
    <NavbarTop />
    <b-container fluid="md" class="mt-5 mb-5">
      <b-row>
        <b-col md="12">
          <b-card class="shadow-md border-o rounded-lg">
            <h5>DATA POSTS</h5>
            <hr>
            <b-button :to="{ name: 'post-create' }" variant="info" class="mb-3">
              TAMBAH
            </b-button>
            <b-table striped bordered hover :items="posts" :fields="fields" show-empty>
              <template v-slot:cell(action)="row">
                <b-button :to="{ name: 'post-edit-id', params: { id: row.item.id } }" variant="warning"
                  size="sm">EDIT</b-button>
              </template>
            </b-table>

          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      //header table
      fields: ['title', 'content', 'action'],
      //posts data
      posts: [],
    }
  },

  mounted() {

    //fetching ke REST API
    this.$axios.get('/api/post')
      .then(response => {


        //assign response ke state "posts"
        this.posts = response.data.data
        // alert(this.posts)

      })

      .catch(error => {
        console.log(error.response.data)
      })

  }

}

</script>

