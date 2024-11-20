<template>
    <form @submit.prevent="handleSubmit">
        <h3>{{ isLoginMode ? 'Logga in' : 'Registrera' }}</h3>
        <label for="email">Email</label>
        <input type="email" v-model="form.email" id="auth-email-input" required>
        <label for="password">Password</label>
        <input type="password" v-model="form.password" id="auth-password-input">
        <label for="confirm-password">Confirm Password</label>
        <input type="password" id="auth-confirm-input" v-model="form.confirmPassword">
        <button type="submit">{{ isLoginMode ? 'Logga in' : 'Registrera' }}</button>
        <p>
            {{ isLoginMode ? 'Har du inget konto?' : 'Har du redan ett konto?' }}
            <button type="button" @click="toggleMode">
                {{ isLoginMode ? 'Registrera' : 'Logga in' }}
            </button>
        </p>
    </form>
</template>

<script>
export default {
 data() {
    return {
        isLoginMode: true,
        form: {
            email: '',
            password: '',
            confirmPassword: '',
        }
    };
 },
 methods: {
    toggleMode() {
        this.isLoginMode = !this.isLoginMode;
    },
    handleSubmit(){
        if (!this.isLoginMode && this.form.password !== this.form.confirmPassword) {
            alert('Lösenord matchar inte!')
            return;
        }

        const payload = {
            email: this.form.email,
            password: this.form.password
        }

        if (this.isLoginMode) {
            console.log('Loggar in:', payload)
        } else {
            console.log('Registrerar:', payload)
        }
    }
 }
}
</script>

<style scoped>
    form {
        width: 20rem;
        padding: 1rem;
        display: flex;
        justify-content: center;
        align-items: first baseline;
        flex-direction: column;
        gap: 1rem;
    }

    button, input {
        background: none;
        border: 1px solid black;
        border-radius: 4px;
    }
</style>