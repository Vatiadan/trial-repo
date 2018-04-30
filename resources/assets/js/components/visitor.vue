<template>
    <div id="app" class="container">

        <form @submit.prevent="submit()" novalidate>
            <legend><strong>Personal Information</strong>  </legend>
            <div class="col-md-12">
                <label class="label">Email</label>
                <p class="control has-icon has-icon-right">
                    <input v-model="edited.email" name="email" v-validate="'required|email'" class="col-md-8" :class="{'input': true, 'is-danger': errors.has('email') }" type="text" placeholder="Email">
                    <i v-show="errors.has('email')" class="fa fa-warning"></i>
                    <span v-show="errors.has('email')" class="help is-danger">{{ errors.first('email') }}</span>
                </p>
            </div>
            <div class="col-md-12">
                <label class="label">First Name</label>
                <p class="control has-icon has-icon-right">
                    <input v-model="name" v-validate="'required|alpha'" class="col-md-8" :class="{'input': true, 'is-danger': errors.has('firstname') }" type="text" data-vv-name="firstname" placeholder="First Name">
                    <i v-show="errors.has('firstname')" class="fa fa-warning"></i>
                    <span v-show="errors.has('firstname')" class="help is-danger">{{ errors.first('firstname') }}</span>
                </p>
            </div>

            <div class="col-md-12">
                <label class="label">Last Name</label>
                <p class="control has-icon has-icon-right">
                    <input v-model="lastname" v-validate="'required|alpha'" class="col-md-8":class="{'input': true, 'is-danger': errors.has('lastname') }" type="text" data-vv-name="lastname" placeholder="Last Name">
                    <i v-show="errors.has('lastname')" class="fa fa-warning"></i>
                    <span v-show="errors.has('lastname')" class="help is-danger">{{ errors.first('lastname') }}</span>

                </p>
            </div>
            <div class="col-md-12">
                <label class="label">County</label>
                <p class="control has-icon has-icon-right">

                    <select name="county">
                    <option value=" ">Please select your County</option>
                    <option> Nairobi</option>
                    <option> Mombasa</option>
                    <option> Nakuru</option>

                    v-model="county" v-validate="'required|alpha'" class="col-md-8":class="{'input': true, 'is-danger': errors.has('county') }"  data-vv-name="county" </select>
                    <i v-show="errors.has('county')" class="fa fa-warning"></i>
                    <span v-show="errors.has('county')" class="help is-danger">{{ errors.first('county') }}</span>
                </p>




            </div>
             <button type="submit" class="btn btn-primary btn-block">Save</button>

            </form>
        </div>



</template>

<script>
    module.exports = {
        data: function () {
            return {
                edited: {
                    email: ''
                },
                firstname: '',
                lastname:'',
                county:''
            }
        }
    }

</script>

<style scoped>



</style>