<template>
  <div class="container">
    <h1>🔐 Connexion</h1>

    <div v-if="error" class="error">{{ error }}</div>
    <div v-if="success" class="success">{{ success }}</div>

    <form @submit.prevent="handleLogin">
      <div class="form-group">
        <label for="email">Email</label>
        <input
          type="email"
          id="email"
          v-model="form.email"
          placeholder="jean.dupont@example.com"
          required
        />
      </div>

      <div class="form-group">
        <label for="password">Mot de passe</label>
        <input
          type="password"
          id="password"
          v-model="form.password"
          placeholder="Votre mot de passe"
          required
        />
      </div>

      <button type="submit" :disabled="loading">
        {{ loading ? 'Connexion...' : 'Se connecter' }}
      </button>
    </form>

    <div class="link">
      Pas encore de compte ? <router-link to="/register">S'inscrire</router-link>
    </div>

    <div class="divider">
      <span>OU</span>
    </div>

    <button @click="signInWithGoogle" type="button" class="google-btn">
      <svg class="google-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
        <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
        <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
        <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
      </svg>
      Se connecter avec Google
    </button>

    <button @click="signInWithGithub" type="button" class="social-btn github-btn">
      <svg class="social-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="">
        <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z" fill="#24292e"/>
      </svg>
      Se connecter avec Github
    </button>

    <button @click="signInWithDiscord" type="button" class="social-btn discord-btn">
      <svg class="social-icon" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" fill="currentColor">
        <path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515a.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0a12.64 12.64 0 0 0-.617-1.25a.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 0 0 .031.057a19.9 19.9 0 0 0 5.993 3.03a.078.078 0 0 0 .084-.028a14.09 14.09 0 0 0 1.226-1.994a.076.076 0 0 0-.041-.106a13.107 13.107 0 0 1-1.872-.892a.077.077 0 0 1-.008-.128a10.2 10.2 0 0 0 .372-.292a.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127a12.299 12.299 0 0 1-1.873.892a.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028a19.839 19.839 0 0 0 6.002-3.03a.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.956-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419c0-1.333.955-2.419 2.157-2.419c1.21 0 2.176 1.096 2.157 2.42c0 1.333-.946 2.418-2.157 2.418z"/>
      </svg>
      Se connecter avec Discord
    </button>
    <div class="jwt-info">
      <h3>💡 Démo JWT</h3>
      <p>
        ✅ Après connexion, un <strong>Access Token</strong> JWT est stocké<br>
        ✅ Ce token est envoyé dans le header <code>Authorization: Bearer ...</code><br>
        ✅ Le serveur vérifie le token sans consulter de session
      </p>
    </div>
  </div>
</template>

<script>
import { authService } from '../services/api'

export default {
  name: 'Login',
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      error: null,
      success: null,
      loading: false
    }
  },
  mounted() {
    // Afficher un message d'erreur si OAuth a échoué
    const error = this.$route.query.error
    if (error === 'google_auth_failed') {
      this.error = 'Échec de l\'authentification Google'
    }else if (error === 'github_auth_failed') {
      this.error = 'Échec de l\'authentification Github'
    }else if (error === 'discord_auth_failed') {
      this.error = 'Échec de l\'authentification Discord'
    }
    else if (error === 'token_generation_failed') {
      this.error = 'Erreur lors de la génération du token'
    }
  },
  methods: {
    async handleLogin() {
      this.error = null
      this.success = null
      this.loading = true

      try {
        const response = await authService.login(this.form)
        this.success = response.message

        // Rediriger vers home après connexion réussie
        setTimeout(() => {
          this.$router.push('/home')
        }, 1000)
      } catch (err) {
        this.error = err.response?.data?.message || 'Erreur lors de la connexion'
      } finally {
        this.loading = false
      }
    },
    signInWithGoogle() {
      // Redirection vers le backend qui initie OAuth
      window.location.href = `${import.meta.env.VITE_API_URL}/auth/google`
    },
    signInWithGithub() {
      window.location.href = `${import.meta.env.VITE_API_URL}/auth/github`
    },
    signInWithDiscord() {
      window.location.href = `${import.meta.env.VITE_API_URL}/auth/discord`
    }
  }
}
</script>

<style scoped>
.divider {
  display: flex;
  align-items: center;
  text-align: center;
  margin: 2rem 0;
  color: #666;
}

.divider::before,
.divider::after {
  content: '';
  flex: 1;
  border-bottom: 1px solid #ddd;
}

.divider span {
  padding: 0 1rem;
  font-size: 0.9rem;
  font-weight: 500;
}

.social-buttons {
  display: flex;
  flex-direction: column;
  font-weight: 500;
}

.social-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  border: 1px solid transparent;
}

.social-icon {
  width: 20px;
  height: 20px;
}

.google-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  background: white;
  color: #3c4043;
  border: 1px solid #dadce0;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.google-btn:hover {
  background: #f8f9fa;
  border-color: #d2d4d6;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}

.google-icon {
  width: 20px;
  height: 20px;
}

.github-btn {
  background: #24292e;
  color: white;
  border-color: #24292e;
}

.github-btn:hover {
  background: #2f363d;
  border-color: #2f363d;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.25);
}

.discord-btn {
  background: #5865F2;
  color: white;
  border-color: #5865F2;
}

.discord-btn:hover {
  background: #4752C4;
  border-color: #4752C4;
  box-shadow: 0 2px 6px rgba(88, 101, 242, 0.3);
}

.jwt-info {
  margin-top: 2rem;
  padding: 1.5rem;
  background: #f0f7ff;
  border-left: 4px solid #2563eb;
  border-radius: 4px;
}

.jwt-info h3 {
  margin: 0 0 0.75rem 0;
  color: #1e40af;
  font-size: 1.1rem;
}

.jwt-info p {
  margin: 0;
  color: #1e3a8a;
  line-height: 1.6;
  font-size: 0.95rem;
}
</style>
