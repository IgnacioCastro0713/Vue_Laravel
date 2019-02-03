<template>
    <div>
        <div class="card">
            <div class="card-header">Editar poema</div>
            <div class="card-body">
                <form method="POST" v-on:submit.prevent="onUpdate">
                    <div class="form-group row">
                        <label for="poem" class="">Poema</label>
                        <input type="text" id="poem" name="poem" class="form-control col-md-12" v-model="form.poem">

                        <label for="autor" class="">Autor</label>
                        <input type="text" id="autor" name="autor" class="form-control col-md-12" v-model="form.autor">
                    </div>
                    <div class="form-group row">
                        <button class="btn btn-info" type="submit">Guardar</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                form: {
                    poem:'',
                    autor:''
                }
            }
        },
        created() {
            let url = '/poem/'.concat(this.$route.params.id).concat('/edit');
            axios.get(url).then((response) => { this.form = response.data; });
        },
        methods: {
            onUpdate() {
                let url = '/poem/'.concat(this.$route.params.id);
                axios.patch(url, this.form).then(() => { this.$router.push({name:'poem-index'})});
            },

        },
    }
</script>

