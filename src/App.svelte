<script>
  import Login from './pages/auth/LoginPage.svelte';
  import Dashboard from './pages/dashboard/DashboardPage.svelte';
  import LandingPage from './pages/landing/LandingPage.svelte';
  import PinusPintarPage from './pages/donasi/PinusPintarPage.svelte';
  import PencairianPage from './pages/donasi/PencairianPage.svelte';

  let isLoggedIn = false;
  let user = null;
  let showLanding = true;
  let showLogin = false;
  let showPinusPintar = false;
  let showPencairian = false;

  function handleLogin(event) {
    user = event.detail;
    isLoggedIn = true;
    showLanding = false;
    showLogin = false;
    showPinusPintar = false;
    showPencairian = false;
  }

  function handleLogout() {
    isLoggedIn = false;
    user = null;
    showLanding = true;
    showLogin = false;
    showPinusPintar = false;
    showPencairian = false;
  }

  function navigateToLogin() {
    showLanding = false;
    showLogin = true;
    showPinusPintar = false;
    showPencairian = false;
  }

  function handleNavigate(event) {
    const { page } = event.detail;
    if (page === 'pinuspintar') {
      showLanding = false;
      showLogin = false;
      showPinusPintar = true;
      showPencairian = false;
    } else if (page === 'pencairian') {
      showLanding = false;
      showLogin = false;
      showPinusPintar = false;
      showPencairian = true;
    } else if (page === 'landing') {
      showLanding = true;
      showLogin = false;
      showPinusPintar = false;
      showPencairian = false;
    }
  }

  function handleBack() {
    showPinusPintar = false;
    showPencairian = false;
    showLanding = true;
    showLogin = false;
  }
</script>

{#if showPencairian}
  <PencairianPage on:back={handleBack} on:navigate={handleNavigate} />
{:else if showPinusPintar}
  <PinusPintarPage on:back={handleBack} on:navigate={handleNavigate} />
{:else if showLanding}
  <LandingPage on:login={navigateToLogin} on:navigate={handleNavigate} />
{:else if showLogin && !isLoggedIn}
  <Login on:login={handleLogin} />
{:else if isLoggedIn}
  <Dashboard {user} logout={handleLogout} />
{/if}

