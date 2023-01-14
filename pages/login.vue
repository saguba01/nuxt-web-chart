<template>
    <div class="container">
        <div class="row justify-content-center" style="height: 100vh;">
            <div class="col-6 d-flex">
                <div class="card my-auto">
                    <div class="card-body">
                        <div class="row">
                            <div class="col-12">
                                <span>Login</span>
                            </div>
                            <div class="col-12">
                                <label for="input-username">username</label>
                                <input type="text" class="form-control" id="input-username" v-model="username">
                            </div>
                            <div class="col-12">
                                <label for="input-password">password</label>
                                <input type="password" class="form-control" id="input-password" v-model="password">
                            </div>
                            <div class="col-12 mt-2">
                                <button class="btn btn-primary btn-block" @click="login">
                                    <span>Login</span>
                                </button>
                            </div>
                            <div class="col-12 mt-2">
                                <button @click="signInWithGoogle" class="btn btn-primary btn-block">Sign in with Google</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            username: '',
            password: ''
        }
    },
    methods: {
        async login() {
            try {
             
                await this.$fire.auth.createUserWithEmailAndPassword(
                this.username,
                this.password
                )
            } catch (e) {
                // handleError(e)
                console.error(e)
            }
        },

        async signInWithGoogle() {
            var provider = new this.$fireModule.auth.GoogleAuthProvider();
            // You can add or remove more scopes here provider.addScope('https://www.googleapis.com/auth/contacts.readonly');
            let authData = await this.$fire.auth.signInWithPopup(provider)
        }
    }
}
</script>