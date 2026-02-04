<script>
  import './pinuspintar.css';
  import { createEventDispatcher } from 'svelte';
  import DonationModal from '../../components/donasi/DonationModal.svelte';
  import profileImg from '../../assets/foto pasbelajar.png';
  import fotoPinos from '../../assets/foto pinos.png';
  import fotoMuncak from '../../assets/foto lagi muncak.jpeg';
  import fotoBeasiswa from '../../assets/foto beasiswa.jpeg';
  import fotoDimasjid from '../../assets/foto dimasjid.jpeg';
  import fotoLampung from '../../assets/foto pas acar lampung.jpeg';
  import fotoMusola from '../../assets/foto di musola.jpeg';
  import fotoMakanSiang from '../../assets/foto makan siang.jpeg';
  // Logo PNG from public folder
  const pinusLogo = '/logo-pinus.png';
  
  const dispatch = createEventDispatcher();
  
  let showDonationModal = false;
  let selectedProgram = 'Program Pinus Pintar';
  
  function handleBack() {
    dispatch('back');
  }
  
  function handleDonate() {
    selectedProgram = 'Program Pinus Pintar';
    showDonationModal = true;
  }
  
  function handleDonateCard(photoId) {
    const photo = photos.find(p => p.id === photoId);
    selectedProgram = photo ? photo.title : 'Program Pinus Pintar';
    showDonationModal = true;
  }
  
  function handleDonationSuccess(event) {
    const donationData = event.detail;
    console.log('Donasi berhasil:', donationData);
    // Di sini bisa ditambahkan logika untuk menyimpan data donasi
  }
  
  function handleModalClose() {
    showDonationModal = false;
  }
  
  function handleDonationComplete() {
    // Navigate ke landing page setelah donasi berhasil
    setTimeout(() => {
      dispatch('navigate', { page: 'landing' });
    }, 1000);
  }
  
  // Array untuk foto-foto dengan caption unik untuk setiap foto - diurutkan dengan benar
  const photos = [
    { 
      id: 1, 
      src: fotoPinos, 
      alt: 'Peserta Program Pinus Pintar - Membangun Pemuda Indonesia Berdaya Dengan Teknologi',
      caption: 'Peserta Program Pinus Pintar - Membangun Pemuda Indonesia Berdaya Dengan Teknologi',
      title: 'Peserta Program Pinus Pintar',
      role: 'Beasiswa Pelatihan Kerja Terampil',
      description: 'Bersama-sama kita membangun pemuda Indonesia yang berdaya dengan teknologi. Program Pinus Pintar memberikan kesempatan bagi generasi muda untuk mengembangkan keterampilan dan siap menghadapi tantangan masa depan melalui pelatihan kerja terampil.'
    },
    { 
      id: 2, 
      src: fotoMuncak, 
      alt: 'Pas Muncak - Kegiatan outdoor peserta Pinus Pintar Hackathon di gunung',
      caption: 'Pas Muncak - Kegiatan outdoor peserta Pinus Pintar Hackathon di gunung',
      title: 'Kegiatan Outdoor Hackathon',
      role: 'Team Building & Kolaborasi',
      description: 'Membangun teamwork dan semangat kolaborasi melalui kegiatan alam terbuka. Kegiatan outdoor ini membantu peserta mengembangkan soft skills dan memperkuat ikatan tim dalam menghadapi tantangan bersama.'
    },
    { 
      id: 3, 
      src: fotoBeasiswa, 
      alt: 'Penerima Beasiswa S1 PinusPintar - Generasi muda yang berprestasi',
      caption: 'Penerima Beasiswa S1 PinusPintar - Generasi muda yang berprestasi',
      title: 'Penerima Beasiswa S1',
      role: 'Beasiswa PinusPintar',
      description: 'Program beasiswa S1 PinusPintar memberikan kesempatan pendidikan tinggi bagi generasi muda yang berprestasi. Setiap penerima beasiswa adalah investasi untuk masa depan Indonesia yang lebih cerah melalui pendidikan teknologi berkualitas.'
    },
    { 
      id: 4, 
      src: fotoDimasjid, 
      alt: 'Awal Mula Pinus Pintar - Belajar Teknologi di Masjid',
      caption: 'Awal Mula Pinus Pintar - Belajar Teknologi di Masjid',
      title: 'Awal Mula Pinus Pintar',
      role: 'Dimulai dari Masjid',
      description: 'Pinus Pintar pertama kali berdiri di masjid untuk mengumpulkan para pemuda belajar teknologi. Dari tempat yang sederhana ini, lahir semangat untuk memberikan akses pendidikan teknologi bagi generasi muda, membuktikan bahwa belajar bisa dimulai dari mana saja dengan niat yang tulus.'
    },
    { 
      id: 5, 
      src: fotoLampung, 
      alt: 'Acara di Lampung - Mengumpulkan Para Pemuda Lampung Belajar Coding',
      caption: 'Acara di Lampung - Mengumpulkan Para Pemuda Lampung Belajar Coding',
      title: 'Acara di Lampung',
      role: 'Ekspansi ke Daerah',
      description: 'Pinus Pintar mengadakan acara di Lampung untuk mengumpulkan para pemuda Lampung belajar coding. Program ini membawa semangat pendidikan teknologi ke berbagai daerah di Indonesia, memberikan kesempatan yang sama bagi pemuda di seluruh nusantara untuk mengembangkan kemampuan teknologi mereka.'
    },
    { 
      id: 6, 
      src: fotoMusola, 
      alt: 'Sholat Dzuhur Bersama dan Obrolan - Melatih Komunikasi untuk Engineer',
      caption: 'Sholat Dzuhur Bersama dan Obrolan - Melatih Komunikasi untuk Engineer',
      title: 'Sholat Dzuhur & Komunikasi',
      role: 'Soft Skills Development',
      description: 'Pas jam istirahat, kita sholat dzuhur bersama. Habis sholat, kita ada obrolan untuk melatih komunikasi biar lancar. Seorang engineer, komunikasi sangat penting di dunia engineer. Program Pinus Pintar tidak hanya mengajarkan coding, tetapi juga membangun kemampuan komunikasi yang esensial untuk kesuksesan di dunia teknologi.'
    },
    { 
      id: 7, 
      src: fotoMakanSiang, 
      alt: 'Makan Siang Gratis - Kebersamaan Tanpa Perbedaan di Pinus Pintar',
      caption: 'Makan Siang Gratis - Kebersamaan Tanpa Perbedaan di Pinus Pintar',
      title: 'Makan Siang Gratis',
      role: 'Kebersamaan & Kesetaraan',
      description: 'Di Pinus Pintar ada makan siang gratis bagi anak yang belajar atau yang sudah bekerja maupun belajar. Kita ada kebersamaan, tidak ada perbedaan, semua sama. Setiap peserta mendapat kesempatan yang sama untuk belajar dan berkembang, terlepas dari latar belakang ekonomi mereka. Kebersamaan ini memperkuat ikatan dan semangat gotong royong dalam mencapai tujuan bersama.'
    }
  ];
  
  let imageErrors = {};
  
  function handleImageError(id) {
    console.log('Image error for photo id:', id);
    imageErrors[id] = true;
  }
  
  // Debug: Log foto yang diimport
  $: {
    if (fotoBeasiswa) {
      console.log('Foto beasiswa loaded:', fotoBeasiswa);
    }
  }
</script>

<div class="pinuspintar-container">
  <!-- Header -->
  <header class="header">
    <div class="header-content">
      <div class="logo">
        <img src={pinusLogo} alt="Logo Pinus Pintar" class="logo-icon" />
        <span class="logo-text">Pinus Pintar</span>
      </div>
      <nav class="header-nav">
        <button type="button" class="nav-link" on:click={() => {
          dispatch('navigate', { page: 'landing' });
        }}>Beranda</button>
        <button type="button" class="nav-link" on:click={() => {
          document.querySelector('.donation-section')?.scrollIntoView({ behavior: 'smooth' });
        }}>Donasi</button>
        <button type="button" class="nav-link" on:click={() => {
          dispatch('navigate', { page: 'pencairian' });
        }}>Galang Dana</button>
        <button type="button" class="nav-link" on:click={() => {
          document.querySelector('.story-section')?.scrollIntoView({ behavior: 'smooth' });
        }}>Tentang Kami</button>
      </nav>
      <div class="header-actions">
        <button type="button" class="search-btn" aria-label="Cari">
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
    <div class="hero-content">
      <h3 class="hero-label">Bantu Mereka</h3>
      <h1 class="hero-title">Donasi Sekarang</h1>
      <p class="hero-subtitle">
        Mereka butuh uluran tangan kita. Karena sedikit bantuan dari kita adalah harapan besar bagi mereka.
      </p>
    </div>
  </section>

  <!-- Donation Cards Section -->
  <section class="donation-section">
    <div class="donation-header">
      <div class="donation-header-left"></div>
      <button class="sort-btn">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <line x1="3" y1="6" x2="21" y2="6"></line>
          <line x1="3" y1="12" x2="21" y2="12"></line>
          <line x1="3" y1="18" x2="21" y2="18"></line>
        </svg>
        URUTKAN
      </button>
    </div>
    
    <div class="donation-grid">
      {#each photos as photo (photo.id)}
        <div class="donation-card" role="button" tabindex="0" on:click={() => handleDonateCard(photo.id)} on:keydown={(e) => e.key === 'Enter' && handleDonateCard(photo.id)}>
          <div class="donation-category">{photo.role}</div>
          <div class="donation-logo">
            <img src={pinusLogo} alt="Logo Pinus Pintar" />
          </div>
          <div class="donation-image-wrapper">
            {#if !imageErrors[photo.id] && photo.src}
              <img 
                src={photo.src} 
                alt={photo.alt}
                class="donation-image"
                on:error={() => handleImageError(photo.id)}
                on:load={() => console.log('Photo loaded:', photo.id, photo.src)}
              />
            {:else}
              <div class="donation-placeholder">
                <svg width="60" height="60" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect>
                  <circle cx="8.5" cy="8.5" r="1.5"></circle>
                  <polyline points="21 15 16 10 5 21"></polyline>
                </svg>
              </div>
            {/if}
          </div>
          <div class="donation-content">
            <h3 class="donation-title">{photo.title}</h3>
            <p class="donation-description">{photo.description}</p>
            <div class="donation-progress">
              <div class="progress-bar">
                <div class="progress-fill" style="width: {Math.floor(Math.random() * 50 + 20)}%"></div>
              </div>
            </div>
            <div class="donation-info">
              <div class="donation-amount">Rp {Math.floor(Math.random() * 5000000 + 100000).toLocaleString('id-ID')} Terkumpul</div>
              <div class="donation-days">{Math.floor(Math.random() * 300 + 30)} Hari Lagi</div>
            </div>
            <div class="donation-organizer">Pinus Pintar</div>
          </div>
        </div>
      {/each}
    </div>
  </section>

  <!-- Story Section -->
  <section class="story-section">
    <div class="story-content">
      <div class="story-header">
        <h2 class="story-title">Cerita dari Hati: Masa Depan Anak-Anak Kita</h2>
        <div class="story-icon">
          <img src={pinusLogo} alt="Logo Pinus Pintar" class="story-logo-img" />
        </div>
      </div>
      
      <div class="story-text">
        <p class="story-paragraph">
          Sebagai orang tua, kita semua memiliki impian yang sama: melihat anak-anak kita tumbuh 
          dengan masa depan yang cerah, penuh peluang, dan bebas dari keterbatasan. Di era digital 
          seperti sekarang, kemampuan coding bukan lagi sekadar keahlian tambahan—melainkan 
          <strong>kunci untuk membuka pintu kesuksesan</strong>.
        </p>
        
        <p class="story-paragraph">
          Program <strong>Pinus Pintar</strong> hadir untuk memberikan kesempatan yang sama kepada 
          anak-anak muda dari berbagai latar belakang. Setiap anak berhak mendapatkan akses pendidikan 
          teknologi terbaik, terlepas dari kondisi ekonomi keluarga mereka. Dengan belajar coding, 
          mereka tidak hanya menguasai bahasa masa depan, tetapi juga membangun kepercayaan diri, 
          kreativitas, dan kemampuan problem-solving yang akan membawa mereka jauh.
        </p>
        
        <div class="story-quote">
          <div class="quote-icon">"</div>
          <p class="quote-text">
            Investasi terbaik yang bisa kita berikan kepada generasi muda adalah pendidikan. 
            Setiap rupiah yang Anda donasikan hari ini, akan menjadi investasi untuk masa depan 
            mereka yang lebih cerah.
          </p>
          <div class="quote-author">— Tim Pinus Pintar</div>
        </div>
        
        <p class="story-paragraph">
          Bayangkan jika anak-anak kita memiliki kesempatan untuk belajar dari mentor berpengalaman, 
          mengembangkan proyek-proyek inovatif, dan membangun jaringan dengan sesama pengembang muda. 
          Mereka tidak hanya akan siap menghadapi dunia kerja, tetapi juga menjadi <strong>agen perubahan</strong> 
          yang membawa dampak positif bagi masyarakat.
        </p>
        
        <p class="story-paragraph highlight-text">
          <strong>Donasi Anda hari ini</strong> bukan hanya sekadar bantuan finansial. Ini adalah 
          <strong>investasi untuk masa depan</strong>—untuk anak-anak yang akan menjadi programmer handal, 
          entrepreneur sukses, atau inovator yang mengubah dunia. Mari bersama-sama kita berikan 
          mereka kesempatan yang mereka pantas dapatkan.
        </p>
      </div>
      
      <div class="story-cta">
        <p class="story-cta-text">Mulai dari sekarang, mari kita wujudkan impian mereka bersama-sama</p>
        <button type="button" class="btn-story-donate" on:click={handleDonate}>
          Berikan Donasi Anda
        </button>
      </div>
    </div>
  </section>

  <!-- Call to Action -->
  <section class="cta-section">
    <div class="cta-content">
      <h2 class="cta-title">Bersama Kita Bisa Membuat Perubahan</h2>
      <p class="cta-description">
        Setiap donasi Anda membantu memberikan akses pendidikan coding untuk anak muda 
        yang membutuhkan. Mari bersama-sama membangun masa depan yang lebih cerah.
      </p>
      <div class="cta-buttons">
        <button type="button" class="btn-donate" on:click={handleDonate}>
          Donasi Sekarang
        </button>
        <button type="button" class="btn-share" on:click={() => {
          if (navigator.share) {
            navigator.share({
              title: 'Pinus Pintar - Support Anak Muda Belajar Koding',
              text: 'Mari kita support anak muda belajar koding melalui program Pinus Pintar',
              url: window.location.href
            }).catch(err => console.log('Error sharing:', err));
          } else {
            alert('Fitur share akan segera tersedia!');
          }
        }}>
          Bagikan Program Ini
        </button>
      </div>
    </div>
  </section>

  <!-- Stats Section -->
  <section class="stats-section">
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-number">500+</div>
        <div class="stat-label">Siswa Terdaftar</div>
      </div>
      <div class="stat-card">
        <div class="stat-number">50+</div>
        <div class="stat-label">Mentor Berpengalaman</div>
      </div>
      <div class="stat-card">
        <div class="stat-number">100+</div>
        <div class="stat-label">Proyek Selesai</div>
      </div>
      <div class="stat-card">
        <div class="stat-number">85%</div>
        <div class="stat-label">Tingkat Kelulusan</div>
      </div>
    </div>
  </section>
  
  <!-- Donation Modal -->
  <DonationModal 
    bind:show={showDonationModal}
    programTitle={selectedProgram}
    on:donate={handleDonationSuccess}
    on:close={handleModalClose}
    on:donationSuccess={handleDonationComplete}
  />
</div>
