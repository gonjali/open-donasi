<script>
  import { createEventDispatcher } from 'svelte';
  import './donation-modal.css';
  
  const dispatch = createEventDispatcher();
  
  export let show = false;
  export let programTitle = 'Program Pinus Pintar';
  
  let donationAmount = '';
  let donorName = '';
  let donorEmail = '';
  let donorPhone = '';
  let donorMessage = '';
  let selectedBank = '';
  let isSubmitting = false;
  
  const banks = [
    
    { value: 'bca', label: 'BCA', account: '0092836655', name: 'Yayasan Pinus Pintar' },
   
  ];
  
  const quickAmounts = [50000, 100000, 250000, 500000, 1000000];
  
  function closeModal() {
    show = false;
    dispatch('close');
  }
  
  // Set nominal cepat dengan format "Rp 100.000"
  function selectAmount(amount) {
    donationAmount = formatCurrency(String(amount));
  }
  
  // Format input menjadi "Rp 100.000" dengan pemisah ribuan Indonesia
  function formatCurrency(value) {
    // Hapus semua karakter selain angka (termasuk Rp dan spasi)
    const numericValue = value.replace(/[^\d]/g, '');
    if (!numericValue) return '';
    
    const num = parseInt(numericValue, 10);
    if (Number.isNaN(num)) return '';
    
    return `Rp ${num.toLocaleString('id-ID')}`;
  }
  
  // Dipanggil setiap kali user mengetik, lalu merapikan kembali nilai
  function handleAmountInput() {
    donationAmount = formatCurrency(donationAmount || '');
  }
  
  async function handleSubmit(e) {
    e.preventDefault();
    
    if (!donationAmount || !donorName || !donorEmail || !donorPhone) {
      alert('Mohon lengkapi semua field yang wajib diisi!');
      return;
    }
    
    isSubmitting = true;
    
    // Simulasi pengiriman data
    setTimeout(() => {
      const donationData = {
        amount: donationAmount.replace(/[^\d]/g, ''),
        name: donorName,
        email: donorEmail,
        phone: donorPhone,
        message: donorMessage,
        bank: selectedBank,
        program: programTitle
      };
      
      console.log('Donasi berhasil:', donationData);
      isSubmitting = false;
      
      // Kirim notifikasi WhatsApp ke admin
      sendWhatsAppNotification(donationData);
      
      // Dispatch event dengan data donasi
      dispatch('donate', donationData);
      
      // Reset form
      donationAmount = '';
      donorName = '';
      donorEmail = '';
      donorPhone = '';
      donorMessage = '';
      selectedBank = '';
      
      // Tutup modal dan tampilkan konfirmasi
      setTimeout(() => {
        show = false;
        dispatch('close');        // Dispatch event untuk navigasi ke landing page setelah donasi berhasil
        dispatch('donationSuccess');
        alert('Terima kasih! Donasi Anda telah direkam. Kami akan menghubungi Anda untuk konfirmasi pembayaran.');
      }, 500);
    }, 1000);
  }
  
  // Fungsi untuk mengirim notifikasi WhatsApp ke admin
  function sendWhatsAppNotification(donationData) {
    const adminPhone = '6281392629799'; // Format internasional tanpa 0
    const bankInfo = banks.find(b => b.value === donationData.bank);
    const bankLabel = bankInfo ? `${bankInfo.label} • ${bankInfo.account}` : donationData.bank || 'Belum dipilih';
    
    // Format jumlah donasi
    const numericAmount = donationData.amount ? donationData.amount.replace(/[^\d]/g, '') : '0';
    const formattedAmount = numericAmount ? `Rp ${parseInt(numericAmount).toLocaleString('id-ID')}` : 'Tidak disebutkan';
    
    const message = `🔔 *LAPORAN DONASI BARU*

📋 *Detail Donasi:*
Program: ${donationData.program}
Jumlah: ${formattedAmount}

👤 *Data Donatur:*
Nama: ${donationData.name}
Email: ${donationData.email}
No. HP/WA: ${donationData.phone}

💳 *Metode Pembayaran:*
Bank: ${bankLabel}

💬 *Pesan:*
${donationData.message || 'Tidak ada pesan'}

---
Terima kasih atas donasinya! 🙏`;

    // Encode pesan untuk URL
    const encodedMessage = encodeURIComponent(message);
    
    // Buat link WhatsApp
    const whatsappUrl = `https://wa.me/${adminPhone}?text=${encodedMessage}`;
    
    // Buka WhatsApp di tab baru
    window.open(whatsappUrl, '_blank');
  }

  // Close modal on escape key
  function handleKeydown(e) {
    if (e.key === 'Escape' && show) {
      closeModal();
    }
  }
</script>

<svelte:window on:keydown={handleKeydown} />

{#if show}
  <div class="modal-overlay" role="dialog" aria-modal="true" aria-labelledby="modal-title" tabindex="-1" on:click={(e) => e.target === e.currentTarget && closeModal()} on:keydown={(e) => e.key === 'Escape' && closeModal()}>
    <div class="modal-content" role="document">
      <button class="modal-close" on:click={closeModal} aria-label="Tutup">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <line x1="18" y1="6" x2="6" y2="18"></line>
          <line x1="6" y1="6" x2="18" y2="18"></line>
        </svg>
      </button>
      
      <div class="modal-header">
        <h2 id="modal-title" class="modal-title">Donasi untuk {programTitle}</h2>
        <p class="modal-subtitle">Setiap donasi Anda membantu memberikan akses pendidikan coding untuk anak muda</p>
      </div>
      
      <form class="donation-form" on:submit={handleSubmit}>
        <div class="form-section">
          <h3 class="form-section-title">Jumlah Donasi</h3>
          <div class="quick-amounts">
            {#each quickAmounts as amount}
              <button 
                type="button" 
                class="quick-amount-btn"
                on:click={() => selectAmount(amount)}
              >
                Rp {amount.toLocaleString('id-ID')}
              </button>
            {/each}
          </div>
          <div class="amount-input-wrapper">
            <input
              type="text"
              class="amount-input"
              placeholder="Rp 0"
              bind:value={donationAmount}
              on:input={handleAmountInput}
              required
            />
          </div>
        </div>
        
        <div class="form-section">
          <h3 class="form-section-title">Data Donatur</h3>
          <div class="form-group">
            <label for="donor-name" class="form-label">
              Nama Lengkap <span class="required">*</span>
            </label>
            <input
              id="donor-name"
              type="text"
              class="form-input"
              placeholder="Masukkan nama lengkap"
              bind:value={donorName}
              required
            />
          </div>
          
          <div class="form-group">
            <label for="donor-email" class="form-label">
              Email <span class="required">*</span>
            </label>
            <input
              id="donor-email"
              type="email"
              class="form-input"
              placeholder="contoh@email.com"
              bind:value={donorEmail}
              required
            />
          </div>
          
          <div class="form-group">
            <label for="donor-phone" class="form-label">
              Nomor HP/WhatsApp <span class="required">*</span>
            </label>
            <input
              id="donor-phone"
              type="tel"
              class="form-input"
              placeholder="0812 3456 7890"
              bind:value={donorPhone}
              required
            />
          </div>
          
          <div class="form-group">
            <label for="donor-bank" class="form-label">
              Pilih Bank Transfer
            </label>
            <select id="donor-bank" class="form-input" bind:value={selectedBank}>
              <option value="">Pilih bank tujuan</option>
              {#each banks as bank}
                <option value={bank.value}>
                  {bank.label} • {bank.account} • {bank.name}
                </option>
              {/each}
            </select>
          </div>
          
          <div class="form-group">
            <label for="donor-message" class="form-label">
              Pesan (Opsional)
            </label>
            <textarea
              id="donor-message"
              class="form-input form-textarea"
              placeholder="Tuliskan pesan atau doa untuk program ini..."
              rows="4"
              bind:value={donorMessage}
            ></textarea>
          </div>
        </div>
        
        <div class="form-actions">
          <button type="button" class="btn-cancel" on:click={closeModal}>
            Batal
          </button>
          <button type="submit" class="btn-submit" disabled={isSubmitting}>
            {#if isSubmitting}
              Mengirim...
            {:else}
              Lanjutkan Donasi
            {/if}
          </button>
        </div>
      </form>
    </div>
  </div>
{/if}
