<template>
  <div class="container">
        <div class="card">
            <div class="card-header">
                <h3>Add Movies</h3>
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="addItem">
                    <div class="row">
                        <div class="col-md-6">
                            <div class="form-group">
                                <label>Movie Name:</label>
                                <input type="text" class="form-control" v-model="item.Title"/>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-group">
                                <label>Year:</label>
                                <input type="text" class="form-control" v-model="item.Year"/>
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <div class="form-group">
                                <label>Imdb ID:</label>
                                <input type="text" class="form-control" v-model="item.imdbID"/>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="form-group">
                                <label>Type:</label>
                                <input type="text" class="form-control" v-model="item.Type"/>
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6">
                            <div class="form-group">
                                <label>Poster:</label>
                                <input type="text" class="form-control" v-model="item.Poster"/>
                            </div>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-6 mt-2">
                            <button class="btn btn-primary">Submit</button>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>
<script>
export default {
  name: 'Create',
  data() {
      return {
          item: {}
      }
  },
  methods: {
      addItem() {
           let uri = 'http://localhost:4000/items/add';
            this.axios.post(uri, this.item).then((response) => {
                console.log(response.data)
            });
        }
    }
}
</script>

