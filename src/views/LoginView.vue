<template>
  <div class="pagina">
    <!-- LADO ESQUERDO: IMAGEM DE FUNDO + LOGO SOBREPOSTO -->
    <section class="lado-imagem">
      <img
        :src="imagemFundo"
        alt="Casa com esquadrias de alumínio"
        class="imagem-fundo"
      />

      <div class="overlay-imagem"></div>

      <div class="conteudo-logo">
        <img
          :src="logoTitulo"
          alt="Logo SA"
          class="logo-titulo"
        />
        <h2>Esquadrias de aluminio</h2>
      </div>
    </section>

    <!-- LADO DIREITO: CARTÃO DE LOGIN -->
    <section class="lado-login">
      <div class="card-login">
        <div class="titulo">
          <h1>Acesse o sistema</h1>
          <p>Informe seus dados para continuar.</p>
        </div>

        <form @submit.prevent="fazerLogin">
          <!-- CAMPO E-MAIL -->
          <div class="campo">
            <svg
              class="icone"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
              <circle cx="12" cy="7" r="4"></circle>
            </svg>

            <input
              v-model.trim="email"
              type="email"
              placeholder="Insira seu Email"
              required
            />
          </div>

          <!-- CAMPO SENHA -->
          <div class="campo">
            <svg
              class="icone"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="1.8"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <rect x="3" y="11" width="18" height="11" rx="2" ry="2"></rect>
              <path d="M7 11V7a5 5 0 0 1 10 0v4"></path>
            </svg>

            <input
              v-model="senha"
              type="password"
              placeholder="Senha"
              required
            />
          </div>

          <!-- BOTÃO ENTRAR -->
          <button type="submit" class="botao-entrar" :disabled="carregando">
            {{ carregando ? 'Entrando...' : 'Entrar' }}
          </button>

          <!-- MENSAGEM DE FEEDBACK -->
          <p v-if="mensagem" :class="['mensagem', tipoMensagem]">
            {{ mensagem }}
          </p>
        </form>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
// Caso você use Vue Router, descomente as duas linhas abaixo:
// import { useRouter } from 'vue-router'
// const router = useRouter()

// Importação das imagens (verifique se os nomes dos arquivos batem com os da sua pasta src)
import imagemFundo from './assets/imagelogin.png'
import logoTitulo from './logotitulo.png'

const email = ref('')
const senha = ref('')
const mensagem = ref('')
const tipoMensagem = ref('erro')
const carregando = ref(false)

const fazerLogin = async () => {
  mensagem.value = ''

  if (!email.value || !senha.value) {
    tipoMensagem.value = 'erro'
    mensagem.value = 'Por favor, preencha todos os campos.'
    return
  }

  carregando.value = true

  try {
    // Simulação de requisição de login (substitua pela sua API ou lógica real)
    await new Promise((resolve) => setTimeout(resolve, 1000))

    // Exemplo de validação simples:
    if (email.value === 'admin@sa.com' && senha.value === '123456') {
      tipoMensagem.value = 'sucesso'
      mensagem.value = 'Login realizado com sucesso! Redirecionando...'
      // router.push('/dashboard')
    } else {
      tipoMensagem.value = 'erro'
      mensagem.value = 'E-mail ou senha incorretos.'
    }
  } catch (error) {
    tipoMensagem.value = 'erro'
    mensagem.value = 'Erro ao conectar com o servidor. Tente novamente.'
  } finally {
    carregando.value = false
  }
}
</script>

<style>
/* Reset global e fontes do protótipo */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Playfair+Display:wght@700&display=swap');

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body,
#app {
  width: 100%;
  min-height: 100vh;
  background-color: #050d21;
  font-family: 'Inter', sans-serif;
  -webkit-font-smoothing: antialiased;
}
</style>

<style scoped>
.pagina {
  display: flex;
  width: 100%;
  min-height: 100vh;
  background-color: #050d21;
}

/* =========================================
   LADO ESQUERDO (IMAGEM + LOGO SOBREPOSTO)
========================================= */
.lado-imagem {
  position: relative;
  width: 45%;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.imagem-fundo {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 1;
}

.overlay-imagem {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.25);
  z-index: 2;
}

.conteudo-logo {
  position: relative;
  z-index: 3;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  margin-top: 130px;
  padding: 0 24px;
}

.logo-titulo {
  width: clamp(95px, 11vw, 135px);
  height: auto;
  margin-bottom: 12px;
}

.conteudo-logo h2 {
  font-family: 'Playfair Display', Georgia, serif;
  color: #ffffff;
  font-size: clamp(1.4rem, 2.2vw, 2.1rem);
  font-weight: 700;
  letter-spacing: 0.4px;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.65);
}

/* =========================================
   LADO DIREITO (FORMULÁRIO DE LOGIN)
========================================= */
.lado-login {
  width: 55%;
  min-height: 100vh;
  background-color: #050d21;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 32px 24px;
}

.card-login {
  background-color: #151d30;
  width: 100%;
  max-width: 460px;
  padding: 52px 44px;
  border-radius: 16px;
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.35);
}

.titulo {
  margin-bottom: 34px;
}

.titulo h1 {
  color: #ffffff;
  font-size: clamp(1.45rem, 2vw, 1.75rem);
  font-weight: 700;
  margin-bottom: 6px;
}

.titulo p {
  color: #cbd5e1;
  font-size: 0.9rem;
}

/* =========================================
   CAMPOS DE INPUT
========================================= */
.campo {
  display: flex;
  align-items: center;
  background-color: #3b4254;
  border-radius: 8px;
  padding: 0 16px;
  height: 50px;
  margin-bottom: 20px;
  border: 1px solid transparent;
  transition: border-color 0.2s ease;
}

.campo:focus-within {
  border-color: #d4b038;
}

.campo .icone {
  width: 18px;
  height: 18px;
  color: #9ca3af;
  margin-right: 12px;
  flex-shrink: 0;
}

.campo input {
  background: transparent;
  border: none;
  outline: none;
  color: #ffffff;
  font-size: 0.92rem;
  width: 100%;
}

.campo input::placeholder {
  color: #9ca3af;
}

/* =========================================
   BOTÃO ENTRAR
========================================= */
.botao-entrar {
  width: 100%;
  height: 50px;
  margin-top: 14px;
  background-color: #d4b038;
  color: #0f172a;
  font-size: 1rem;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease, opacity 0.2s ease;
}

.botao-entrar:hover:not(:disabled) {
  background-color: #e0bd46;
}

.botao-entrar:active:not(:disabled) {
  transform: scale(0.99);
}

.botao-entrar:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

/* =========================================
   MENSAGENS DE ERRO / SUCESSO
========================================= */
.mensagem {
  margin-top: 16px;
  text-align: center;
  font-size: 0.88rem;
  font-weight: 500;
}

.mensagem.erro {
  color: #f87171;
}

.mensagem.sucesso {
  color: #4ade80;
}

/* =========================================
   RESPONSIVIDADE (TABLET E CELULAR)
========================================= */
@media (max-width: 900px) {
  .pagina {
    flex-direction: column;
  }

  .lado-imagem {
    width: 100%;
    min-height: 260px;
    height: 32vh;
  }

  .conteudo-logo {
    margin-top: 0;
  }

  .lado-login {
    width: 100%;
    min-height: auto;
    flex: 1;
    padding: 32px 20px 48px;
  }
}

@media (max-width: 480px) {
  .lado-imagem {
    min-height: 210px;
    height: 28vh;
  }

  .card-login {
    padding: 36px 24px;
    border-radius: 14px;
  }

  .titulo {
    margin-bottom: 26px;
  }

  .campo,
  .botao-entrar {
    height: 46px;
  }
}
</style>