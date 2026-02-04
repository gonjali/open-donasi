<script>
  import './pencairian.css';
  import { createEventDispatcher, onMount, onDestroy } from 'svelte';
  import fotoPinos from '../../assets/foto pinos.png';
  import fotoMuncak from '../../assets/foto lagi muncak.jpeg';
  import fotoBeasiswa from '../../assets/foto beasiswa.jpeg';
  import fotoDimasjid from '../../assets/foto dimasjid.jpeg';
  import fotoBersamaPinusPintar from '../../assets/foto_bersama_pinus_pintar.png';
  import fotoPasbelajar from '../../assets/foto pasbelajar.png';
  import fotoLampung from '../../assets/foto pas acar lampung.jpeg';
  import fotoMusola from '../../assets/foto di musola.jpeg';
  import fotoMakanSiang from '../../assets/foto makan siang.jpeg';
  
  const pinusLogo = '/logo-pinus.png';
  const dispatch = createEventDispatcher();
  
  let searchQuery = '';
  let showScrollTop = false;
  let selectedCategory = '';
  let imageErrors = {};
  
  function handleImageError(campaignId) {
    imageErrors[campaignId] = true;
  }
  
  function handleScroll() {
    showScrollTop = window.scrollY > 300;
  }
  
  onMount(() => {
    if (typeof window !== 'undefined') {
      window.addEventListener('scroll', handleScroll);
    }
  });
  
  onDestroy(() => {
    if (typeof window !== 'undefined') {
      window.removeEventListener('scroll', handleScroll);
    }
  });
  
  const popularSearches = [
    { id: 1, label: 'Pendidikan', icon: '📚' },
    { id: 2, label: 'Beasiswa', icon: '🎓' },
    { id: 3, label: 'Teknologi', icon: '💻' },
    { id: 4, label: 'Pemuda', icon: '👥' },
    { id: 5, label: 'Pelatihan', icon: '🔧' }
  ];
  
  const campaigns = [
    {
      id: 1,
      category: 'Pendidikan',
      categoryColor: '#f97316',
      image: fotoBersamaPinusPintar,
      title: 'Program Beasiswa Pelatihan Kerja Terampil - Teach4Hope',
      description: 'Bersama-sama kita membangun pemuda Indonesia yang berdaya dengan teknologi. Program Pinus Pintar bekerjasama dengan Teach4Hope dan Kitabisa-ORG memberikan kesempatan bagi generasi muda untuk mengembangkan keterampilan dan siap menghadapi tantangan masa depan melalui pelatihan kerja terampil.',
      collaborator: 'Bersama Teach4Hope & Kitabisa-ORG',
      url: 'pinuspintar.com/beasiswa-pelatihan',
      funds: 4208456,
      donors: 316
    },
    {
      id: 2,
      category: 'Pendidikan',
      categoryColor: '#f97316',
      image: fotoPasbelajar,
      title: 'Sesi Pelatihan Teknologi - Workshop Coding',
      description: 'Sesi pelatihan teknologi aktif dengan peserta yang antusias belajar coding dan teknologi. Program ini memberikan kesempatan hands-on learning dengan mentor berpengalaman untuk mengembangkan keterampilan teknologi peserta.',
      collaborator: 'Bersama Teach4Hope',
      url: 'pinuspintar.com/workshop-coding',
      funds: 1408295,
      donors: 332
    },
    {
      id: 3,
      category: 'Pendidikan',
      categoryColor: '#f97316',
      image: fotoLampung,
      title: 'Pinus Pintar Lampung - Membangun Pemuda Indonesia Berdaya dengan Teknologi',
      description: 'Program ekspansi Pinus Pintar ke Lampung untuk mengumpulkan para pemuda Lampung belajar coding dan teknologi. Program ini membawa semangat pendidikan teknologi ke berbagai daerah di Indonesia, memberikan kesempatan yang sama bagi pemuda di seluruh nusantara.',
      collaborator: 'Bersama Komunitas Lampung',
      url: 'pinuspintar.com/lampung',
      funds: 325043,
      donors: 26
    },
    {
      id: 4,
      category: 'Pendidikan',
      categoryColor: '#f97316',
      image: fotoPinos,
      title: 'Peserta Program Pinus Pintar - Komunitas Pembelajar',
      description: 'Peserta Program Pinus Pintar yang berdedikasi untuk membangun pemuda Indonesia yang berdaya dengan teknologi. Program ini memberikan kesempatan bagi generasi muda untuk mengembangkan keterampilan teknologi dan membangun jaringan profesional.',
      collaborator: 'Bersama Tim Pinus Pintar',
      url: 'pinuspintar.com/peserta',
      funds: 203000,
      donors: 1452
    },
    {
      id: 5,
      category: 'Pendidikan',
      categoryColor: '#f97316',
      image: fotoBeasiswa,
      title: 'Bantu 25 Anak Panti Belajar Teknologi',
      description: 'Program pendidikan teknologi untuk anak-anak panti asuhan. Setiap anak berhak mendapatkan akses pendidikan teknologi terbaik, terlepas dari kondisi ekonomi keluarga mereka.',
      collaborator: 'Bersama Yayasan Pinus Pintar',
      url: 'pinuspintar.com/panti-teknologi',
      funds: 1850000,
      donors: 245
    },
    {
      id: 6,
      category: 'Pendidikan',
      categoryColor: '#f97316',
      image: fotoDimasjid,
      title: 'Awal Mula Pinus Pintar - Belajar di Masjid',
      description: 'Pinus Pintar pertama kali berdiri di masjid untuk mengumpulkan para pemuda belajar teknologi. Dari tempat yang sederhana ini, lahir semangat untuk memberikan akses pendidikan teknologi.',
      collaborator: 'Bersama Komunitas Masjid',
      url: 'pinuspintar.com/masjid-teknologi',
      funds: 890000,
      donors: 128
    },
    {
      id: 7,
      category: 'Sosial',
      categoryColor: '#f97316',
      image: fotoMusola,
      title: 'Sholat Dzuhur Bersama dan Komunikasi - Soft Skills Development',
      description: 'Pas jam istirahat, kita sholat dzuhur bersama. Habis sholat, kita ada obrolan untuk melatih komunikasi biar lancar. Seorang engineer, komunikasi sangat penting di dunia engineer.',
      collaborator: 'Bersama Komunitas Masjid',
      url: 'pinuspintar.com/soft-skills',
      funds: 1560000,
      donors: 189
    },
    {
      id: 8,
      category: 'Sosial',
      categoryColor: '#f97316',
      image: fotoMakanSiang,
      title: 'Makan Siang Gratis - Kebersamaan Tanpa Perbedaan',
      description: 'Di Pinus Pintar ada makan siang gratis bagi anak yang belajar atau yang sudah bekerja maupun belajar. Kita ada kebersamaan, tidak ada perbedaan, semua sama.',
      collaborator: 'Bersama Yayasan Pinus Pintar',
      url: 'pinuspintar.com/makan-siang',
      funds: 203000,
      donors: 1452
    },
    {
      id: 9,
      category: 'Sosial',
      categoryColor: '#f97316',
      image: fotoMuncak,
      title: 'Kegiatan Outdoor Hackathon Pemuda',
      description: 'Membangun teamwork dan semangat kolaborasi melalui kegiatan alam terbuka. Kegiatan outdoor ini membantu peserta mengembangkan soft skills dan memperkuat ikatan tim.',
      collaborator: 'Bersama Komunitas Developer',
      url: 'pinuspintar.com/hackathon-outdoor',
      funds: 203000,
      donors: 1452
    },
    {
      id: 10,
      category: 'Pendidikan',
      categoryColor: '#f97316',
      image: fotoBersamaPinusPintar,
      title: 'Pinus Pintar Lampung - Kolaborasi Teach4Hope & Kitabisa-ORG',
      description: 'Kolase kegiatan Pinus Pintar Lampung yang menampilkan berbagai aktivitas program pendidikan teknologi. Dari sesi pelatihan indoor, foto bersama peserta program beasiswa, hingga kegiatan outdoor di lokasi Pinus Pintar Lampung. Program ini membawa semangat "Membangun Pemuda Indonesia Berdaya dengan Teknologi" ke berbagai daerah.',
      collaborator: 'Bersama Teach4Hope & Kitabisa-ORG',
      url: 'pinuspintar.com/lampung-collage',
      funds: 2500000,
      donors: 450
    }
  ];
  
  function handleBack() {
    dispatch('back');
  }
  
  function handleSearch(e) {
    console.log('=== SEARCH BUTTON CLICKED ===');
    console.log('Event:', e);
    console.log('Search query:', searchQuery);
    
    if (e) {
      e.preventDefault();
      e.stopPropagation();
    }
    
    alert(`Tombol pencarian diklik! Mencari: ${searchQuery || 'Semua Campaign'}`);
    
    // Implement search logic
    return false;
  }
  
  function handleCategoryClick(category) {
    selectedCategory = selectedCategory === category ? '' : category;
    console.log('Selected category:', selectedCategory);
  }
  
  function handleCampaignClick(campaign) {
    console.log('Campaign clicked:', campaign);
    // Navigate to donation page with selected campaign
    dispatch('navigate', { page: 'pinuspintar', campaign: campaign.id });
  }
  
  function scrollToTop() {
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
</script>

<div class="pencairian-container">
  <!-- Header -->
  <header class="pencairian-header">
    <div class="header-content">
      <div class="logo">
        <img src={pinusLogo} alt="Logo Pinus Pintar" class="logo-icon" />
        <span class="logo-text">Pinus Pintar</span>
      </div>
      <nav class="header-nav">
        <button type="button" class="nav-link" on:click={() => dispatch('navigate', { page: 'landing' })}>Beranda</button>
        <button type="button" class="nav-link" on:click={() => dispatch('navigate', { page: 'pinuspintar' })}>Donasi</button>
        <button type="button" class="nav-link active" on:click={() => {
          // Already on Galang Dana page, scroll to top
          window.scrollTo({ top: 0, behavior: 'smooth' });
        }}>Galang Dana</button>
        <button type="button" class="nav-link" on:click={() => dispatch('navigate', { page: 'pinuspintar' })}>Tentang Kami</button>
      </nav>
      <div class="header-actions">
        <button 
          type="button" 
          class="search-btn" 
          on:click={handleSearch}
          aria-label="Cari"
        >
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="8"></circle>
            <path d="m21 21-4.35-4.35"></path>
          </svg>
        </button>
        <button type="button" class="login-btn">Masuk</button>
        <button type="button" class="back-btn-mobile" on:click={handleBack} aria-label="Kembali">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M19 12H5M12 19l-7-7 7-7"/>
          </svg>
        </button>
      </div>
    </div>
  </header>

  <!-- Hero Section -->
  <section class="hero-section">
    <div class="hero-background" style="background-image: url('{fotoBersamaPinusPintar}');">
      <div class="hero-overlay"></div>
    </div>
    <div class="hero-content">
      <h1 class="hero-title">Cari Campaign</h1>
      <div class="search-wrapper">
        
        <input
          type="text"
          class="search-input"
          placeholder="Cari Campaign.."
          bind:value={searchQuery}
          on:keydown={(e) => e.key === 'Enter' && handleSearch()}
        />
        <button 
          type="button" 
          class="search-submit-btn" 
          on:click={handleSearch}
          aria-label="Cari"
        >
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="8"></circle>
            <path d="m21 21-4.35-4.35"></path>
          </svg>
        </button>
      </div>
    </div>
  </section>

  <!-- Popular Searches Section -->
  <section class="popular-searches-section">
    <div class="section-container">
      <h2 class="section-title">Pencarian Populer</h2>
      <div class="popular-searches">
        {#each popularSearches as search}
          <button
            type="button"
            class="popular-search-btn"
            class:active={selectedCategory === search.label}
            on:click={() => handleCategoryClick(search.label)}
          >
            <span class="search-icon">{search.icon}</span>
            <span class="search-label">{search.label}</span>
          </button>
        {/each}
      </div>
    </div>
  </section>

  <!-- Popular Campaigns Section -->
  <section class="campaigns-section">
    <div class="section-container">
      <h2 class="section-title">Campaign Populer</h2>
      <div class="campaigns-grid">
        {#each campaigns as campaign}
          <div class="campaign-card" role="button" tabindex="0" on:click={() => handleCampaignClick(campaign)} on:keydown={(e) => e.key === 'Enter' && handleCampaignClick(campaign)}>
            <div class="campaign-category" style="background-color: {campaign.categoryColor}20; color: {campaign.categoryColor};">
              {campaign.category}
            </div>
            <div class="campaign-image-wrapper">
              {#if !imageErrors[campaign.id] && campaign.image}
                <img 
                  src={campaign.image} 
                  alt={campaign.title} 
                  class="campaign-image"
                  on:error={() => handleImageError(campaign.id)}
                />
              {:else}
                <div class="campaign-image-placeholder">
                  <svg width="60" height="60" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect>
                    <circle cx="8.5" cy="8.5" r="1.5"></circle>
                    <polyline points="21 15 16 10 5 21"></polyline>
                  </svg>
                </div>
              {/if}
            </div>
            <div class="campaign-content">
              <h3 class="campaign-title">{campaign.title}</h3>
              <p class="campaign-description">{campaign.description}</p>
              <div class="campaign-collaborator">
                {campaign.collaborator}
              </div>
              <div class="campaign-url">{campaign.url}</div>
              <div class="campaign-stats">
                <div class="campaign-funds">
                  <span class="funds-amount">Rp {campaign.funds.toLocaleString('id-ID')}</span>
                </div>
                <div class="campaign-donors">
                  <span class="donors-count">{campaign.donors}</span>
                </div>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Scroll to Top Button -->
  {#if showScrollTop}
    <button type="button" class="scroll-top-btn" on:click={scrollToTop} aria-label="Kembali ke atas">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M18 15l-6-6-6 6"/>
      </svg>
    </button>
  {/if}
</div>
