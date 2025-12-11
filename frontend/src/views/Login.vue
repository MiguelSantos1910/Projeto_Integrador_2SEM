<template>
    <div class="container">
        <div class="form-section">
            <div class="form-wrapper">
                <h1>Seja Bem-Vindo!</h1>
                <h2>Login</h2>

                <form @submit.prevent="handleLogin">
                    <div class="form-group">
                        <label for="email">E-mail ou usuário:</label>
                        <input
                            type="email"
                            id="email"
                            v-model="email"
                            required
                        />
                    </div>

                    <div class="form-group">
                        <label for="senha">Senha:</label>
                        <input
                            type="password"
                            id="senha"
                            v-model="password"
                            required
                        />
                    </div>

                    <div class="remember">
                        <input
                            type="checkbox"
                            id="idRemember"
                            v-model="rememberMe"
                        />
                        <label for="idRemember">Lembrar minha senha</label>
                    </div>

                    <button type="submit">Entrar</button>

                    <p class="register">
                        Não possui conta?
                        <RouterLink to="/cadastro">Cadastre-se</RouterLink>
                    </p>
                </form>
            </div>
        </div>

        <div class="image-section">
            <img src="/src/assets/loginsucos.png" alt="Sucos" />
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { RouterLink, useRouter } from "vue-router";
import { useUsuarioStore } from "../stores/usuario";

const email = ref("");
const password = ref("");
const rememberMe = ref(false);

const store = useUsuarioStore();
const router = useRouter();

async function handleLogin() {
    try {
        // 1. Tenta fazer login. A Store deve cuidar de buscar o token e o usuário (incluindo role).
        const ok = await store.login({
            email: email.value,
            password: password.value,
        });

        if (!ok) {
            alert("Falha no login: Credenciais inválidas.");
            return; // Sai da função se o login falhar
        }
        
        // Se o login foi OK, o objeto 'store.usuario' deve estar populado.
        
        // 2. Verifica o papel (role) e redireciona. 
        // A checagem simplificada deve ser suficiente.
        if (store.usuario?.role === "admin") {
            router.push({ name: "AdminDashboard" });
        } else {
            router.push({ name: "home" });
        }

        // 3. Lógica "Lembrar-me" (Mantida)
        if (rememberMe.value) {
            localStorage.setItem("rememberEmail", email.value);
        } else {
            localStorage.removeItem("rememberEmail");
        }

    } catch (err) {
        // Captura erros de rede ou exceções não tratadas no Store
        alert("Ocorreu um erro ao conectar: " + err.message);
        console.error(`Erro ao fazer login: ${err.message}`);
    }
}
</script>

<style scoped>
/* Os estilos permanecem inalterados e estão otimizados. */
.container {
    display: flex;
    min-height: 100vh;
    font-family: "Montserrat", sans-serif;
}

.form-section {
    flex: 1;
    padding: 40px;
    background: linear-gradient(to bottom, #ffeded, #c7e4f3);

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.form-wrapper {
    width: 100%;
    max-width: 500px;
}

h1 {
    font-size: 32px;
    font-weight: 700;
    color: #ff8c1a;
    margin-bottom: 10px;
}

h2 {
    font-size: 24px;
    color: #333;
    margin-bottom: 30px;
}

form {
    display: flex;
    flex-direction: column;
    width: 100%;
}

.form-group {
    display: flex;
    flex-direction: column;
    margin-bottom: 15px;
}

.form-group label {
    margin-bottom: 8px;
    font-weight: 600;
    color: #555;
}

input[type="email"],
input[type="password"] {
    width: 100%;
    padding: 14px 20px;
    border: 1px solid #ccc;
    border-radius: 25px;
    outline: none;
    font-size: 16px;
    box-sizing: border-box;
    transition: all 0.3s ease;
}

input[type="email"]:focus,
input[type="password"]:focus {
    border-color: #ff8c1a;
    box-shadow: 0 0 0 3px rgba(255, 140, 26, 0.2);
}

.remember {
    display: flex;
    align-items: center;
    margin: 10px 0 20px 0;
    color: #555;
}

.remember label {
    margin-left: 8px;
    font-size: 14px;
}

button {
    width: 100%;
    padding: 14px;
    border: none;
    background-color: #ff8c1a;
    color: white;
    font-size: 16px;
    font-weight: 700;
    text-transform: uppercase;
    border-radius: 25px;
    cursor: pointer;
    transition: all 0.3s ease;
    margin-bottom: 20px;
}

button:hover {
    background-color: #ff7b00;
    transform: translateY(-3px);
    box-shadow: 0 4px 15px rgba(255, 123, 0, 0.3);
}

.register {
    text-align: center;
    font-size: 15px;
}

.register a {
    color: #ff8c1a;
    font-weight: bold;
    text-decoration: none;
}
.register a:hover {
    text-decoration: underline;
}

.image-section {
    flex: 1;
    background-color: #f5f5f5;
    display: flex;
}

.image-section img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

@media (max-width: 800px) {
    .image-section {
        display: none;
    }
    .form-section {
        flex-basis: 100%;
    }
}
</style>