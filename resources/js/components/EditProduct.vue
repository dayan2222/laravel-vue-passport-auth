<template>
    <div>
        <h3 class="text-center"> Create Product</h3>
        <div class="row">
            <div class="col-md-6">
                <form @submit.prevent="updateProduct">
                    <div class="form-group">
                        <label>Name</label>
                        <input type="text" class="form-control" v-model="product.name">
                    </div>
                    <div class="form-group">
                        <label>Detail</label>
                        <input type="text" class="form-control" v-model="product.detail">
                    </div>
                    <button type="submit" class="btn btn-primary">Create</button>

                </form>
            </div>
        </div>        
    </div>    
</template>

<script>


    export default {
        data(){
            return{
                product:{},
                user: this.auth.user

            }
        },
        created(){
            this.axios
                .get(`http://localhost:8000/api/products/${this.$route.params.id}`)
                .then(response=>{
                    this.product = response.data;
                });
        },
        methods:{
            updateProduct(){
                this.axios
                    .patch(`http://localhost:8000/api/products/${this.$route.params.id}`, this.product)
                    .then(response=>(
                        this.$router.push({ name: 'Products' })
                    )).catch(err => console.log(err))
                .finally(() => this.loading = false)
            }
        }
    }
    
</script>
