<template>
    <form action="" class="mt-5" @submit.prevent="registerUser">
        <div class="form-group">
            <label for="email">Ваш email:</label>
            <input type="email" class="form-control" id="email" placeholder="Введите email:" required v-model="user.email">
        </div>
        <div class="form-group">
            <label for="password">Ваш пароль (минимум 6 символов):</label>
            <input type="password" class="form-control" id="password" placeholder="Введите пароль:" required v-model="user.password">
        </div>
        <div class="form-group">
            <label for="password2">Повторите пароль:</label>
            <input type="password" class="form-control" id="password" placeholder="Повторите пароль:" required v-model="user.confirmPassword">
        </div>
        <div class="alert alert-danger" role="alert" v-if="error">
            <strong>Упс!</strong> Пароли не совпадают или их длинна меньше 6 символов.
        </div>
        <button type="submit" class="btn btn-primary">Зарегистрироваться</button>
    </form>
</template>

<script>
    export default {
        name: 'sign-up',
        data() {
            return {
                user: {
                    email: '',
                    password: '',
                    confirmPassword: ''
                },
                error: false,

            }
        },
        methods: {
            registerUser() {
                if(this.user.password !== this.user.confirmPassword || this.user.password.length < 6) {
                    this.error = true;
                } else {
                    firebase.auth().createUserWithEmailAndPassword(this.user.email, this.user.password)
                        .then( () => {
                            this.$emit('regSuccess', 'sign-in');
                        })
                        .cath( error => {
                            console.log(error);
                        })
                }
            } 
        }
    }
</script>
