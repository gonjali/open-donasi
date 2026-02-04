<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let email = 'admin@opendonasi.id';
  let password = 'admin';

  function submitForm() {
    if (email.trim() && password.trim()) {
      dispatch('login', {
        name: 'Admin Open Donasi',
        email
      });
    } else {
      alert('Isi email dan password dulu ya.');
    }
  }
</script>

<div class="login-page">
  <div class="login-card">
    <div class="login-logo">
      <span class="logo-icon">◎</span>
      <span class="logo-text">Open Donasi</span>
    </div>

    <h1>Masuk ke Dashboard</h1>
    <p class="subtitle">Kelola kampanye dan donasi dengan mudah.</p>

    <form on:submit|preventDefault={submitForm}>
      <label>
        <span>Email</span>
        <input
          type="email"
          bind:value={email}
          placeholder="admin@opendonasi.id"
          required
        />
      </label>

      <label>
        <span>Password</span>
        <input
          type="password"
          bind:value={password}
          placeholder="••••••••"
          required
        />
      </label>

      <button type="submit">Masuk</button>
    </form>

    <p class="hint">Untuk demo, pakai email dan password apa saja.</p>
  </div>
</div>

<style>
  .login-page {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: radial-gradient(circle at top, #1f2937 0, #020617 55%);
    color: #e5e7eb;
    padding: 16px;
  }

  .login-card {
    width: 100%;
    max-width: 420px;
    background: rgba(15, 23, 42, 0.95);
    border-radius: 18px;
    padding: 28px 26px 26px;
    box-shadow: 0 24px 60px rgba(0, 0, 0, 0.65);
    border: 1px solid rgba(148, 163, 184, 0.25);
  }

  .login-logo {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 18px;
  }

  .logo-icon {
    width: 28px;
    height: 28px;
    border-radius: 999px;
    background: linear-gradient(135deg, #22c55e, #16a34a);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    color: white;
  }

  .logo-text {
    font-weight: 600;
    letter-spacing: 0.02em;
  }

  h1 {
    font-size: 1.4rem;
    margin: 0 0 4px;
  }

  .subtitle {
    margin: 0 0 20px;
    font-size: 0.9rem;
    color: #9ca3af;
  }

  form {
    display: flex;
    flex-direction: column;
    gap: 14px;
    margin-bottom: 12px;
  }

  label {
    display: flex;
    flex-direction: column;
    gap: 6px;
    font-size: 0.85rem;
    color: #cbd5f5;
  }

  input {
    padding: 9px 11px;
    border-radius: 10px;
    border: 1px solid #1f2937;
    background: #020617;
    color: #e5e7eb;
    font-size: 0.9rem;
    outline: none;
  }

  input:focus {
    border-color: #22c55e;
    box-shadow: 0 0 0 1px rgba(34, 197, 94, 0.4);
  }

  button {
    margin-top: 8px;
    padding: 10px 14px;
    border-radius: 999px;
    border: none;
    background: linear-gradient(135deg, #22c55e, #16a34a);
    color: white;
    font-weight: 600;
    font-size: 0.95rem;
    cursor: pointer;
    transition: transform 0.06s ease, box-shadow 0.06s ease, opacity 0.06s;
    box-shadow: 0 14px 35px rgba(34, 197, 94, 0.35);
  }

  button:hover {
    transform: translateY(-1px);
    box-shadow: 0 18px 45px rgba(34, 197, 94, 0.45);
  }

  button:active {
    transform: translateY(0);
    box-shadow: 0 10px 24px rgba(34, 197, 94, 0.35);
    opacity: 0.94;
  }

  .hint {
    margin: 0;
    font-size: 0.78rem;
    color: #6b7280;
    text-align: center;
  }

  @media (max-width: 480px) {
    .login-card {
      padding: 22px 18px 20px;
      border-radius: 16px;
    }
  }
</style>

