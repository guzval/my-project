<template>
    
</template>

<script>
    import {db} from '@/main';
    import * as faker from 'faker';
    import {mapGetters} from 'vuex';
    export default {
        name: "admin-users-dialog",
        methods: {
            close () {
                this.$store.commit('toggleUsersDialog', {
                    editMode: false,
                    user: {
                        uid: null,
                        email: '',
                        username: ''
                    }
                })                
            },
            add () {
                this.userForEdit.uid = faker.random.alphaNumeric(16);
                this.userForEdit.role = 'customer';
                const user = Object.assign({}, this.userForEdit);
                db.collection('users').doc(this.userForEdit.uid).set(user).then (() => {
                    this.$store.commit('setAlertMessage', {
                        show: true,
                        type: 'success',
                        message: this.$t('messages.saved', {item: this.$t('common.user')}),
                        timeout: 5000
                    });
                    this.close();
                })
            },
            update () {
                const user = Object.assign({}, this.userForEdit);
                db.collection('users').doc(user.uid).update(user).then (() => {
                    this.$store.commit('setAlertMessage', {
                        show: true,
                        type: 'success',
                        message: this.$t('messages.updated', {item: this.$t('common.user')}),
                        timeout: 5000
                    });
                    this.close();
                })
            }
        },
        computed: {
            userDialog: {
                get() {
                    return this.$store.getters.usersDialog;
                },
                set() {
                    this.close();
                }
            },
            ...mapGetters(['userForEdit'])
        }
    }
</script>


