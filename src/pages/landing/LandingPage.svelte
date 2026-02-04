<script>
  import './landing.css';
  import { createEventDispatcher, onMount, onDestroy } from 'svelte';
  import fotoBersamaPinusPintar from '../../assets/foto_bersama_pinus_pintar.png';
  import fotoPasbelajar from '../../assets/foto pasbelajar.png';
  import fotoPinos from '../../assets/foto pinos.png';
  import fotoBeasiswa from '../../assets/foto beasiswa.jpeg';
  import fotoLampung from '../../assets/foto pas acar lampung.jpeg';
  
  const dispatch = createEventDispatcher();
  
  // Logo PNG from public folder
  const pinusLogo = '/logo-pinus.png';
  
  // Carousel images
  const carouselImages = [
    {
      src: fotoBersamaPinusPintar,
      title: 'Program Beasiswa Pelatihan Kerja Terampil',
      description: 'Bersama-sama kita membangun pemuda Indonesia yang berdaya dengan teknologi'
    },
    {
      src: fotoPasbelajar,
      title: 'Sesi Pelatihan Teknologi',
      description: 'Workshop coding aktif dengan peserta yang antusias belajar teknologi'
    },
    {
      src: fotoPinos,
      title: 'Peserta Program Pinus Pintar',
      description: 'Komunitas pembelajar yang berdedikasi untuk membangun pemuda Indonesia'
    },
    {
      src: fotoBeasiswa,
      title: 'Penerima Beasiswa S1',
      description: 'Generasi muda yang berprestasi mendapatkan kesempatan pendidikan tinggi'
    },
    {
      src: fotoLampung,
      title: 'Pinus Pintar Lampung',
      description: 'Ekspansi program ke berbagai daerah di Indonesia'
    }
  ];
  
  let currentSlide = 0;
  let autoPlayInterval;
  
  function nextSlide() {
    currentSlide = (currentSlide + 1) % carouselImages.length;
  }
  
  function prevSlide() {
    currentSlide = (currentSlide - 1 + carouselImages.length) % carouselImages.length;
  }
  
  function goToSlide(index) {
    currentSlide = index;
  }
  
  function startAutoPlay() {
    autoPlayInterval = setInterval(() => {
      nextSlide();
    }, 5000); // Ganti slide setiap 5 detik
  }
  
  function stopAutoPlay() {
    if (autoPlayInterval) {
      clearInterval(autoPlayInterval);
    }
  }
  
  onMount(() => {
    startAutoPlay();
  });
  
  onDestroy(() => {
    stopAutoPlay();
  });
  
  function handleDonate() {
    // Navigate to donation page
    dispatch('navigate', { page: 'pinuspintar' });
  }
  
  function handleFundraise() {
    // Navigate to fundraising page
    console.log('Navigate to fundraising');
    dispatch('navigate', { page: 'pencairian' });
  }
  
  function handleLoginClick() {
    dispatch('login');
  }
</script>

<div class="landing-container">
  <!-- Header -->
  <header class="header">
    <div class="header-content">
      <div class="logo">
        <img src={pinusLogo} alt="Logo DonasiKita" class="logo-icon" />
        <span class="logo-text">DonasiKita</span>
      </div>
      
      <nav class="nav-menu">
        <a href="#home" class="nav-link">Beranda</a>
        <a href="#donasi" class="nav-link">Donasi</a>
        <a href="#galang-dana" class="nav-link">Galang Dana</a>
        <a href="#tentang" class="nav-link">Tentang Kami</a>
      </nav>
      
      <div class="header-actions">
        <button class="search-btn" aria-label="Search">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="8"></circle>
            <path d="m21 21-4.35-4.35"></path>
          </svg>
        </button>
        <button class="login-btn" on:click={handleLoginClick}>Masuk</button>
      </div>
    </div>
  </header>

  <!-- Hero Section -->
  <main class="hero-section">
    <div class="hero-content">
      <!-- Left Content -->
      <div class="hero-left">
        <div class="hero-badge">
          <span>Platform Donasi & Galang Dana Terpercaya</span>
        </div>
        
        <h1 class="hero-title">
          Bersama Kita Membangun
          <span class="highlight">#MasaDepanLebihBaik</span>
        </h1>
        
        <p class="hero-description">
          Platform donasi dan galang dana online yang memudahkan Anda untuk berbagi kebaikan 
          dan membantu sesama kapan saja, di mana saja. Mari wujudkan perubahan positif bersama.
        </p>
        
        <div class="cta-buttons">
          <button type="button" class="btn-primary" on:click={handleDonate}>
            Mulai Donasi
          </button>
          <button type="button" class="btn-secondary" on:click={handleFundraise}>
            Galang Dana
          </button>
        </div>
        
        <!-- App Download Section -->
        <div class="app-download">
          <p class="app-download-title">Unduh Aplikasi DonasiKita</p>
          <div class="app-badges">
            <button type="button" class="app-badge google-play">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path d="M3,20.5V3.5C3,2.91 3.34,2.39 3.84,2.15L13.69,12L3.84,21.85C3.34,21.6 3,21.09 3,20.5M16.81,15.12L6.05,21.34L14.54,12.85L16.81,15.12M20.16,10.81C20.5,11.08 20.75,11.5 20.75,12C20.75,12.5 20.53,12.9 20.18,13.18L17.89,14.5L15.39,12L17.89,9.5L20.16,10.81M6.05,2.66L16.81,8.88L14.54,11.15L6.05,2.66Z"/>
              </svg>
              <div>
                <span class="badge-label">GET IT ON</span>
                <span class="badge-name">Google Play</span>
              </div>
            </button>
            <button type="button" class="app-badge app-store">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                <path d="M18.71,19.5C17.88,20.74 17,21.95 15.66,21.97C14.32,22 13.89,21.18 12.37,21.18C10.84,21.18 10.37,21.95 9.1,22C7.79,22.05 6.8,20.68 5.96,19.47C4.25,17 2.94,12.45 4.7,9.39C5.57,7.87 7.13,6.91 8.82,6.88C10.1,6.86 11.32,7.75 12.11,7.75C12.89,7.75 14.37,6.68 15.92,6.84C16.57,6.87 18.39,7.1 19.58,8.82C19.47,8.88 17.39,10.1 17.41,12.63C17.44,15.65 20.06,16.66 20.09,16.67C20.06,16.74 19.67,18.11 18.71,19.5M13,3.5C13.73,2.67 14.94,2.04 15.94,2C16.07,3.17 15.6,4.35 14.9,5.19C14.21,6.04 13.07,6.7 11.95,6.61C11.8,5.46 12.36,4.26 13,3.5Z"/>
              </svg>
              <div>
                <span class="badge-label">Download on the</span>
                <span class="badge-name">App Store</span>
              </div>
            </button>
            <button type="button" class="app-badge appgallery">
              <div class="appgallery-badge">
                <span>EXPLORE IT ON</span>
                <span class="appgallery-text">AppGallery</span>
              </div>
            </button>
          </div>
        </div>
      </div>
      
      <!-- Right Visual Content -->
      <div class="hero-right">
        <div class="image-gallery">
          <div class="carousel-container" on:mouseenter={stopAutoPlay} on:mouseleave={startAutoPlay}>
            <div class="carousel-wrapper">
              {#each carouselImages as image, index}
                <div class="carousel-slide" class:active={currentSlide === index}>
                  <div class="image-card image-card-main">
                    <img 
                      src={image.src} 
                      alt={image.title}
                      class="hero-image"
                    />
                  </div>
                  
                  <!-- Content Card -->
                  <div class="image-content-card">
                    <div class="image-badge">🌲 Teknologi</div>
                    <h3 class="image-title">{image.title}</h3>
                    <p class="image-description">{image.description}</p>
                  </div>
                </div>
              {/each}
            </div>
            
            <!-- Navigation Buttons -->
            <button class="carousel-btn carousel-prev" on:click={prevSlide} aria-label="Previous">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M19 12H5M12 19l-7-7 7-7"/>
              </svg>
            </button>
            <button class="carousel-btn carousel-next" on:click={nextSlide} aria-label="Next">
              <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M5 12h14M12 5l7 7-7 7"/>
              </svg>
            </button>
            
            <!-- Indicator Dots -->
            <div class="carousel-indicators">
              {#each carouselImages as _, index}
                <button 
                  class="carousel-dot" 
                  class:active={currentSlide === index}
                  on:click={() => goToSlide(index)}
                  aria-label="Go to slide {index + 1}"
                ></button>
              {/each}
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</div>
