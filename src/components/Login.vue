<template>
    <div>
        <auth-form action="login" v-on:process="login($event)" />
        <app-snack-bar
            v-if="snackBar"
            :snackBar="snackBar"
            :text="message"
            :timeout="timeout"
        />   
    </div>    
</template>

<script>
    import AuthForm from '@/forms/Auth';
    import AppSnackBar from '@/components/SnackBar';
    import {db} from '@/main';
    export default {
        name: "Login",
        components:{AuthForm, AppSnackBar},
        data () {
            return {
                snackBar: false,
                message: '',
                timeout: 5000
            }
        },
        methods: {
            login (user) {
                this.$store.dispatch('firebaseLogin',user).then(data => {
                    db.collection('users').doc(data.user.uid).onSnapshot(snapshot => {
                        console.log(snapshot.data());
                        this.$router.push('/');
                    })
                })
                .catch ((error) => {
                    this.message = error.message.substr(0,200);
                    this.snackBar = true;
                    setTimeout(() => {
                        this.snackBar = false;
                    }, this.timeout);
                })
            }
        }
    }
</script>

