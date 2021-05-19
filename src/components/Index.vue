<template>
    <div>
        <button class="btn btn-primary" id="show-modal" @click="showModal = true" style="float:right">Add Movie</button>
        <h1>Movies</h1>
        <div>Search: <input name="search" placeholder="Enter Movie to Search" @change="fetchItems" v-model="search"></div>
        <br>
        <table class="table table-hover table-bordered">
            <thead>
            <tr>
                <td style="text-align:center;">ID</td>
                <td style="text-align:center;">Title</td>
                <td style="text-align:center;">Year</td>
                <td style="text-align:center;">Imdb ID</td>
                <td style="text-align:center;">Type</td>
                <td style="text-align:center;">Poster</td>
            </tr>
            </thead>
                <tbody v-if="items">
                    <tr v-for="(item,index) in items" :key="index">
                        <td style="vertical-align:middle; text-align:center;">{{ ++index }}</td>
                        <td style="vertical-align:middle; text-align:center;">{{ item.Title }}</td>
                        <td style="vertical-align:middle; text-align:center;">{{ item.Year }}</td>
                        <td style="vertical-align:middle; text-align:center;">{{ item.imdbID }}</td>
                        <td style="vertical-align:middle; text-align:center;">{{ item.Type }}</td>
                        <td style="vertical-align:middle; text-align:center;"><img :src="item.Poster" width="90px" alt=""></td>
                    </tr>
                </tbody>
                <tbody v-else>
                    <tr>
                        <td style="vertical-align:middle; text-align:center;" colspan="6">No Data Available</td>
                    </tr>
                </tbody>
        </table>
        <div id="app">
            <div v-if="showModal">
                <transition name="modal">
                <div class="modal-mask">
                    <div class="modal-wrapper">
                    <div class="modal-dialog">
                        <div class="modal-content">
                        <div class="modal-header">
                            <button type="button" class="close btn btn-danger btn-small" @click="showModal=false">
                                <span aria-hidden="true">&times;</span>
                            </button>
                            <h4 class="modal-title">Add New Movies</h4>
                        </div>
                        <div class="modal-body">
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
                                            <button type="submit" class="btn btn-primary">Submit</button>
                                        </div>
                                    </div>
                                </form>
                            </div>
                        </div>
                        </div>
                    </div>
                    </div>
                </div>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        data(){
            return{
                items: [],
                search: "",
                showModal: false,
                item: {}
            }
        },

        created: function()
        {
            this.fetchItems();
        },

        methods: {
            fetchItems()
            {
                let uri = "";
                if(this.search == "")
                {
                    uri = 'http://www.omdbapi.com/?apikey=e0620bd4&s=batman';
                }else{
                    uri = 'http://www.omdbapi.com/?apikey=e0620bd4&s='+this.search;
                }

              this.axios.get(uri).then((response) => {
                  this.items = response.data.Search;
              });
            },
            addItem()
            {
                this.items.unshift(this.item);
                this.item = {};
                this.showModal = false;
            }
        }
    }
</script>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

</style>