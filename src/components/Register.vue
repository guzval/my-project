<template>
    <div>

        <auth-form
          action="register"
          v-on:process="register($event)"
        />

        <app-snack-bar
            v-if="snackBar"
            :snack-bar="snackBar"
            :text="message"
            :timeout="timeout"
        />
        
    </div>
</template>

<script>
import AppSnackBar from '@/components/SnackBar';
import AuthForm from '@/forms/Auth';
export default {
    name: "Register",
    components: {AuthForm, AppSnackBar},
    data () {
        return {
            snackBar: false,
            message: '',
            timeout: 5000
        }
    },
    methods: {
        register (user) {
            console.log(user);
        }
    }
}
</script>

