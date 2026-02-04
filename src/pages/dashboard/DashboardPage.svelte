<script>
  export let user;
  export let logout;

  let activeMenu = 'Dashboard';

  const stats = [
    { label: 'Total Donasi', value: '1.250', sub: 'IDR 125.450.000', accent: 'green' },
    { label: 'Donasi Baru', value: '320', sub: 'Bulan Ini', accent: 'blue' },
    { label: 'Kampanye Aktif', value: '8', sub: 'Sedang Berjalan', accent: 'indigo' },
    { label: 'Penarikan Dana', value: 'IDR 15.200.000', sub: 'Dalam Proses', accent: 'amber' }
  ];

  const recentCampaigns = [
    { title: 'Renovasi Sekolah', progress: 75, color: '#22c55e' },
    { title: 'Bantuan Medis', progress: 42, color: '#3b82f6' },
    { title: 'Proyek Air Bersih', progress: 66, color: '#a855f7' }
  ];

  const latestDonations = [
    { name: 'Budi Santoso', amount: 'IDR 500.000', method: 'Transfer Bank', date: '08/05/2024' },
    { name: 'Siti Rahmawati', amount: 'IDR 200.000', method: 'Kartu Kredit', date: '08/05/2024' },
    { name: 'Andi Wijaya', amount: 'IDR 1.750.000', method: 'QRIS', date: '07/05/2024' },
    { name: 'Maria Lestari', amount: 'IDR 150.000', method: 'E-Wallet', date: '07/05/2024' }
  ];

  const topDonors = [
    { name: 'Rina Permana', total: 'IDR 15.000.000' },
    { name: 'David Wirawan', total: 'IDR 12.500.000' },
    { name: 'Arief Hadi', total: 'IDR 10.000.000' }
  ];

  const donors = [
    { name: 'Rina Permana', email: 'rina@example.com', total: 'IDR 15.000.000', count: 12, lastDonation: '08/05/2024', status: 'Aktif' },
    { name: 'David Wirawan', email: 'david@example.com', total: 'IDR 12.500.000', count: 8, lastDonation: '07/05/2024', status: 'Aktif' },
    { name: 'Arief Hadi', email: 'arief@example.com', total: 'IDR 10.000.000', count: 15, lastDonation: '08/05/2024', status: 'Aktif' },
    { name: 'Budi Santoso', email: 'budi@example.com', total: 'IDR 8.500.000', count: 6, lastDonation: '08/05/2024', status: 'Aktif' },
    { name: 'Siti Rahmawati', email: 'siti@example.com', total: 'IDR 7.200.000', count: 9, lastDonation: '08/05/2024', status: 'Aktif' },
    { name: 'Andi Wijaya', email: 'andi@example.com', total: 'IDR 6.800.000', count: 5, lastDonation: '07/05/2024', status: 'Aktif' },
    { name: 'Maria Lestari', email: 'maria@example.com', total: 'IDR 5.500.000', count: 7, lastDonation: '06/05/2024', status: 'Aktif' },
    { name: 'Joko Susilo', email: 'joko@example.com', total: 'IDR 4.200.000', count: 4, lastDonation: '05/05/2024', status: 'Aktif' }
  ];

  function handleLogout() {
    logout && logout();
  }
</script>

<div class="layout">
  <aside class="sidebar">
    <div class="brand">
      <div class="brand-icon">◎</div>
      <div class="brand-text">
        <span class="brand-name">Open Donasi</span>
        <span class="brand-sub">Admin Panel</span>
      </div>
    </div>

    <nav class="menu">
      <button
        class="menu-item"
        class:active={activeMenu === 'Dashboard'}
        on:click={() => (activeMenu = 'Dashboard')}
      >
        Dashboard
      </button>
      <button
        class="menu-item"
        class:active={activeMenu === 'Donasi'}
        on:click={() => (activeMenu = 'Donasi')}
      >
        Donasi
      </button>
      <button
        class="menu-item"
        class:active={activeMenu === 'Donatur'}
        on:click={() => (activeMenu = 'Donatur')}
      >
        Donatur
      </button>
      <button
        class="menu-item"
        class:active={activeMenu === 'Laporan'}
        on:click={() => (activeMenu = 'Laporan')}
      >
        Laporan
      </button>
      <button
        class="menu-item"
        class:active={activeMenu === 'Pengaturan'}
        on:click={() => (activeMenu = 'Pengaturan')}
      >
        Pengaturan
      </button>
    </nav>

    <button class="logout" on:click={handleLogout}>
      <span class="logout-icon">⏻</span>
      <span class="logout-label">Keluar</span>
    </button>
  </aside>

  <main class="main">
    <header class="topbar">
      <div>
        <h1>{activeMenu === 'Dashboard' ? 'Dashboard Donasi' : activeMenu}</h1>
        <p>Selamat datang, {user?.name ?? 'Admin'}.</p>
      </div>
      <div class="user-pill">
        <div class="avatar">{(user?.name ?? 'A').slice(0, 1)}</div>
        <div class="user-info">
          <span class="user-name">{user?.name ?? 'Admin Open Donasi'}</span>
          <span class="user-role">Super Admin</span>
        </div>
      </div>
    </header>

    {#if activeMenu === 'Dashboard'}
      <section class="stats-row">
        {#each stats as s}
          <article class={`stat-card ${s.accent}`}>
            <p class="stat-label">{s.label}</p>
            <p class="stat-value">{s.value}</p>
            <p class="stat-sub">{s.sub}</p>
          </article>
        {/each}
      </section>

      <section class="grid">
        <article class="panel span-2">
          <header class="panel-head">
            <h2>Ringkasan Donasi</h2>
            <button class="chip">30 Hari Terakhir</button>
          </header>
          <div class="chart-placeholder">
            <div class="chart-lines">
              <div class="line"></div>
              <div class="line"></div>
              <div class="line"></div>
            </div>
            <div class="chart-bars">
              {#each Array(8) as _, i}
                <div class="bar" style={`height: ${40 + i * 5}%`}></div>
              {/each}
            </div>
          </div>
        </article>

        <article class="panel">
          <header class="panel-head">
            <h2>Donatur Terbaru</h2>
          </header>
          <ul class="campaign-list">
            {#each recentCampaigns as c}
              <li>
                <div>
                  <p class="title">{c.title}</p>
                  <div class="progress">
                    <div
                      class="progress-inner"
                      style={`width:${c.progress}%;background:${c.color};`}
                    ></div>
                  </div>
                </div>
                <span class="progress-text">{c.progress}% tercapai</span>
              </li>
            {/each}
          </ul>
        </article>

        <article class="panel span-2">
          <header class="panel-head">
            <h2>Donasi Terbaru</h2>
          </header>
          <table class="table">
            <thead>
              <tr>
                <th>Donatur</th>
                <th>Nominal</th>
                <th>Metode</th>
                <th>Tanggal</th>
              </tr>
            </thead>
            <tbody>
              {#each latestDonations as d}
                <tr>
                  <td>{d.name}</td>
                  <td>{d.amount}</td>
                  <td>{d.method}</td>
                  <td>{d.date}</td>
                </tr>
              {/each}
            </tbody>
          </table>
        </article>

        <article class="panel">
          <header class="panel-head">
            <h2>Donatur Teratas</h2>
          </header>
          <ul class="donor-list">
            {#each topDonors as d}
              <li>
                <div class="avatar small">
                  {d.name.slice(0, 1)}
                </div>
                <div class="donor-info">
                  <p class="title">{d.name}</p>
                  <p class="muted">{d.total}</p>
                </div>
              </li>
            {/each}
          </ul>
        </article>
      </section>
    {:else if activeMenu === 'Donasi'}
      <section class="donation-layout">
        <article class="panel span-2">
          <header class="panel-head">
            <h2>Buat Donasi Baru</h2>
          </header>

          <form class="donation-form">
            <div class="form-row">
              <label class="field">
                <span>Nama Donatur</span>
                <input type="text" placeholder="Masukkan nama lengkap" />
              </label>
            </div>

            <div class="form-row two-col">
              <label class="field">
                <span>Pilih Nomor Rekening</span>
                <select>
                  <option>– Pilih rekening tujuan –</option>
                  <option>BRI • 1234 5678 90 • Yayasan Open Donasi</option>
                  <option>BCA • 9876 5432 10 • Yayasan Open Donasi</option>
                  <option>Mandiri • 5555 2222 11 • Yayasan Open Donasi</option>
                </select>
              </label>

              <label class="field">
                <span>Tanggal Donasi</span>
                <input type="date" />
              </label>
            </div>

            <div class="form-row two-col">
              <label class="field">
                <span>Nomor HP</span>
                <input type="tel" placeholder="Contoh: 0812 3456 7890" />
              </label>

              <label class="field">
                <span>Jumlah Transaksi Terakhir (IDR)</span>
                <input type="number" min="0" placeholder="Contoh: 250000" />
              </label>
            </div>

            <div class="form-row">
              <label class="field">
                <span>Alamat</span>
                <textarea rows="3" placeholder="Masukkan alamat lengkap donatur"></textarea>
              </label>
            </div>

            <div class="form-row">
              <label class="field">
                <span>Status</span>
                <div class="status-toggle">
                  <label>
                    <input type="radio" name="status-donasi" checked />
                    <span class="pill active-pill">Aktif</span>
                  </label>
                  <label>
                    <input type="radio" name="status-donasi" />
                    <span class="pill inactive-pill">Non Aktif</span>
                  </label>
                </div>
              </label>
            </div>

            <div class="form-actions">
              <button type="button" class="btn-secondary">Batal</button>
              <button type="submit" class="btn-primary">Simpan Donasi</button>
            </div>
          </form>
        </article>
      </section>
    {:else if activeMenu === 'Donatur'}
      <section class="donation-layout">
        <article class="panel span-2">
          <header class="panel-head">
            <h2>Daftar Donatur</h2>
            <button class="chip">Total: {donors.length} Donatur</button>
          </header>
          <table class="table">
            <thead>
              <tr>
                <th>Nama</th>
                <th>Email</th>
                <th>Total Donasi</th>
                <th>Jumlah Donasi</th>
                <th>Donasi Terakhir</th>
                <th>Status</th>
              </tr>
            </thead>
            <tbody>
              {#each donors as donor}
                <tr>
                  <td>{donor.name}</td>
                  <td>{donor.email}</td>
                  <td>{donor.total}</td>
                  <td>{donor.count}x</td>
                  <td>{donor.lastDonation}</td>
                  <td>
                    <span class="status-badge" class:active={donor.status === 'Aktif'}>
                      {donor.status}
                    </span>
                  </td>
                </tr>
              {/each}
            </tbody>
          </table>
        </article>
      </section>
    {:else if activeMenu === 'Laporan'}
      <section class="donation-layout">
        <article class="panel span-2">
          <header class="panel-head">
            <h2>Laporan Donasi</h2>
            <button class="chip">Bulan Ini</button>
          </header>
          <table class="table">
            <thead>
              <tr>
                <th>Tanggal</th>
                <th>Kampanye</th>
                <th>Jumlah Donasi</th>
                <th>Total Donatur</th>
                <th>Status</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>08/05/2024</td>
                <td>Program Pinus Pintar</td>
                <td>IDR 5.250.000</td>
                <td>45</td>
                <td><span class="status-badge active">Aktif</span></td>
              </tr>
              <tr>
                <td>07/05/2024</td>
                <td>Beasiswa Pelatihan Kerja</td>
                <td>IDR 3.800.000</td>
                <td>32</td>
                <td><span class="status-badge active">Aktif</span></td>
              </tr>
              <tr>
                <td>06/05/2024</td>
                <td>Renovasi Sekolah</td>
                <td>IDR 8.200.000</td>
                <td>68</td>
                <td><span class="status-badge active">Aktif</span></td>
              </tr>
              <tr>
                <td>05/05/2024</td>
                <td>Bantuan Medis</td>
                <td>IDR 2.500.000</td>
                <td>28</td>
                <td><span class="status-badge active">Aktif</span></td>
              </tr>
            </tbody>
          </table>
        </article>
      </section>
    {:else if activeMenu === 'Pengaturan'}
      <section class="donation-layout">
        <article class="panel span-2">
          <header class="panel-head">
            <h2>Pengaturan Sistem</h2>
          </header>
          <form class="donation-form">
            <div class="form-row">
              <label class="field">
                <span>Nama Organisasi</span>
                <input type="text" value="Open Donasi" placeholder="Masukkan nama organisasi" />
              </label>
            </div>
            <div class="form-row">
              <label class="field">
                <span>Email Kontak</span>
                <input type="email" value="admin@opendonasi.id" placeholder="Masukkan email kontak" />
              </label>
            </div>
            <div class="form-row">
              <label class="field">
                <span>Nomor Telepon</span>
                <input type="tel" value="+62 812 3456 7890" placeholder="Masukkan nomor telepon" />
              </label>
            </div>
            <div class="form-row">
              <label class="field">
                <span>Alamat</span>
                <textarea rows="3" placeholder="Masukkan alamat lengkap">Jl. Contoh No. 123, Jakarta</textarea>
              </label>
            </div>
            <div class="form-actions">
              <button type="button" class="btn-secondary">Batal</button>
              <button type="submit" class="btn-primary">Simpan Pengaturan</button>
            </div>
          </form>
        </article>
      </section>
    {:else}
      <section class="placeholder">
        <article class="panel span-2">
          <header class="panel-head">
            <h2>{activeMenu}</h2>
          </header>
          <p class="placeholder-text">
            Halaman {activeMenu.toLowerCase()} belum ada fitur lengkapnya. Di sini nanti kamu bisa
            menambahkan form dan tabel sesuai kebutuhan.
          </p>
        </article>
      </section>
    {/if}
  </main>
</div>

<style>
  .layout {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 240px minmax(0, 1fr);
    background: radial-gradient(circle at top left, #1f2937 0, #020617 50%);
    color: #e5e7eb;
  }

  .sidebar {
    padding: 20px 18px;
    border-right: 2px solid rgba(31, 41, 55, 0.95);
    background: rgba(15, 23, 42, 0.98);
    display: flex;
    flex-direction: column;
    gap: 20px;
    box-shadow: 2px 0 8px rgba(0, 0, 0, 0.3);
  }

  .brand {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .brand-icon {
    width: 32px;
    height: 32px;
    border-radius: 10px;
    background: linear-gradient(135deg, #22c55e, #3b82f6);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
  }

  .brand-text {
    display: flex;
    flex-direction: column;
  }

  .brand-name {
    font-weight: 600;
    color: #e5e7eb;
  }

  .brand-sub {
    font-size: 0.75rem;
    color: #9ca3af;
    font-weight: 500;
  }

  .menu {
    display: flex;
    flex-direction: column;
    gap: 6px;
    margin-top: 12px;
  }

  .menu-item {
    text-align: left;
    padding: 10px 12px;
    border-radius: 8px;
    border: none;
    background: transparent;
    color: #d1d5db;
    font-size: 0.95rem;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s ease;
    border-left: 3px solid transparent;
  }

  .menu-item:hover {
    background: rgba(31, 41, 55, 0.9);
    color: #ffffff;
    border-left-color: rgba(34, 197, 94, 0.5);
  }

  .menu-item.active {
    background: rgba(34, 197, 94, 0.15);
    color: #22c55e;
    font-weight: 600;
    border-left-color: #22c55e;
  }

  .logout {
    margin-top: auto;
    width: 100%;
    padding: 10px 14px;
    border-radius: 999px;
    border: none;
    background: linear-gradient(135deg, #22c55e, #16a34a);
    color: white;
    font-weight: 600;
    font-size: 0.95rem;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    box-shadow: 0 14px 35px rgba(34, 197, 94, 0.35);
    transition: transform 0.06s ease, box-shadow 0.06s ease, opacity 0.06s;
  }

  .logout-icon {
    width: 18px;
    height: 18px;
    border-radius: 999px;
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.7rem;
    background: rgba(0, 0, 0, 0.12);
  }

  .logout-label {
    letter-spacing: 0.02em;
  }

  .logout:hover {
    transform: translateY(-1px);
    box-shadow: 0 18px 45px rgba(34, 197, 94, 0.45);
  }

  .logout:active {
    transform: translateY(0);
    box-shadow: 0 10px 24px rgba(34, 197, 94, 0.35);
  }

  .main {
    padding: 18px 22px 26px;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .topbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .topbar h1 {
    margin: 0 0 4px;
    font-size: 1.4rem;
  }

  .topbar p {
    margin: 0;
    font-size: 0.9rem;
    color: #9ca3af;
  }

  .user-pill {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 6px 10px;
    background: rgba(15, 23, 42, 0.95);
    border-radius: 999px;
    border: 1px solid rgba(148, 163, 184, 0.4);
  }

  .avatar {
    width: 28px;
    height: 28px;
    border-radius: 999px;
    background: linear-gradient(135deg, #22c55e, #16a34a);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.85rem;
  }

  .avatar.small {
    width: 30px;
    height: 30px;
    font-size: 0.86rem;
  }

  .user-info {
    display: flex;
    flex-direction: column;
  }

  .user-name {
    font-size: 0.85rem;
  }

  .user-role {
    font-size: 0.7rem;
    color: #9ca3af;
  }

  .stats-row {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    gap: 10px;
  }

  .stat-card {
    padding: 12px 14px;
    border-radius: 14px;
    background: rgba(15, 23, 42, 0.95);
    border: 1px solid rgba(31, 41, 55, 0.9);
  }

  .stat-card .stat-label {
    font-size: 0.8rem;
    color: #9ca3af;
    margin: 0 0 4px;
  }

  .stat-card .stat-value {
    font-size: 1.2rem;
    font-weight: 600;
    margin: 0 0 2px;
  }

  .stat-card .stat-sub {
    font-size: 0.8rem;
    color: #6b7280;
    margin: 0;
  }

  .stat-card.green {
    border-color: rgba(34, 197, 94, 0.6);
  }
  .stat-card.blue {
    border-color: rgba(59, 130, 246, 0.6);
  }
  .stat-card.indigo {
    border-color: rgba(79, 70, 229, 0.6);
  }
  .stat-card.amber {
    border-color: rgba(245, 158, 11, 0.6);
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 12px;
    align-items: start;
  }

  .donation-layout {
    display: grid;
    grid-template-columns: minmax(0, 1fr);
    gap: 12px;
    margin-top: 8px;
  }

  .donation-form {
    display: flex;
    flex-direction: column;
    gap: 14px;
    margin-top: 6px;
  }

  .form-row {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .form-row.two-col {
    flex-direction: row;
    gap: 12px;
  }

  .form-row.two-col .field {
    flex: 1;
  }

  .field {
    display: flex;
    flex-direction: column;
    gap: 6px;
    font-size: 0.84rem;
    color: #cbd5f5;
  }

  .field span {
    font-weight: 500;
  }

  .field input,
  .field select,
  .field textarea {
    border-radius: 10px;
    border: 1px solid rgba(31, 41, 55, 0.9);
    background: #020617;
    color: #e5e7eb;
    padding: 8px 10px;
    font-size: 0.88rem;
    outline: none;
    resize: vertical;
  }

  .field input:focus,
  .field select:focus,
  .field textarea:focus {
    border-color: #22c55e;
    box-shadow: 0 0 0 1px rgba(34, 197, 94, 0.35);
  }

  .form-actions {
    margin-top: 4px;
    display: flex;
    justify-content: flex-end;
    gap: 10px;
  }

  .btn-primary,
  .btn-secondary {
    border-radius: 999px;
    border: 1px solid transparent;
    padding: 7px 14px;
    font-size: 0.86rem;
    font-weight: 500;
    cursor: pointer;
  }

  .btn-primary {
    background: linear-gradient(135deg, #22c55e, #16a34a);
    color: white;
    box-shadow: 0 10px 24px rgba(34, 197, 94, 0.4);
  }

  .btn-secondary {
    background: rgba(15, 23, 42, 0.95);
    color: #e5e7eb;
    border-color: rgba(148, 163, 184, 0.6);
  }

  .btn-primary:hover {
    box-shadow: 0 14px 32px rgba(34, 197, 94, 0.55);
  }

  .btn-secondary:hover {
    background: rgba(31, 41, 55, 0.95);
  }

  .status-toggle {
    display: inline-flex;
    gap: 8px;
    padding: 4px;
    border-radius: 999px;
    background: rgba(15, 23, 42, 0.95);
    border: 1px solid rgba(55, 65, 81, 0.9);
  }

  .status-toggle > label {
    position: relative;
    cursor: pointer;
  }

  .status-toggle input {
    position: absolute;
    opacity: 0;
    pointer-events: none;
  }

  .pill {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 4px 10px;
    border-radius: 999px;
    font-size: 0.78rem;
  }

  .active-pill {
    background: linear-gradient(135deg, #22c55e, #16a34a);
    color: white;
  }

  .inactive-pill {
    background: rgba(31, 41, 55, 0.9);
    color: #9ca3af;
  }

  .panel {
    background: rgba(15, 23, 42, 0.98);
    border-radius: 16px;
    border: 1px solid rgba(31, 41, 55, 0.9);
    padding: 14px 14px 16px;
    overflow-x: auto;
  }

  .panel .table {
    margin-top: 10px;
    width: 100%;
  }

  .panel.span-2 {
    grid-column: span 2;
  }

  .panel-head {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }

  .panel-head h2 {
    margin: 0;
    font-size: 0.98rem;
  }

  .chip {
    border-radius: 999px;
    border: none;
    padding: 4px 10px;
    font-size: 0.75rem;
    background: rgba(15, 23, 42, 0.9);
    color: #9ca3af;
  }

  .chart-placeholder {
    border-radius: 12px;
    border: 1px dashed rgba(55, 65, 81, 0.9);
    padding: 10px;
    display: grid;
    grid-template-columns: 40px minmax(0, 1fr);
    gap: 12px;
    align-items: flex-end;
  }

  .chart-lines {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 120px;
  }

  .chart-lines .line {
    height: 1px;
    background: rgba(55, 65, 81, 0.9);
  }

  .chart-bars {
    display: flex;
    align-items: flex-end;
    gap: 6px;
    height: 120px;
  }

  .chart-bars .bar {
    flex: 1;
    background: linear-gradient(180deg, #22c55e, #0f766e);
    border-radius: 6px 6px 0 0;
  }

  .campaign-list,
  .donor-list {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .campaign-list li,
  .donor-list li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
  }

  .title {
    margin: 0 0 2px;
    font-size: 0.9rem;
  }

  .muted {
    margin: 0;
    font-size: 0.78rem;
    color: #9ca3af;
  }

  .progress {
    position: relative;
    width: 140px;
    height: 5px;
    border-radius: 999px;
    background: #020617;
    overflow: hidden;
  }

  .progress-inner {
    height: 100%;
    border-radius: inherit;
  }

  .progress-text {
    font-size: 0.8rem;
    color: #9ca3af;
  }

  .table {
    width: 100% !important;
    min-width: 600px !important;
    border-collapse: separate !important;
    border-spacing: 0 !important;
    font-size: 0.9rem !important;
    color: #e5e7eb !important;
    display: table !important;
    margin-top: 10px !important;
    border: 1px solid rgba(148, 163, 184, 0.3) !important;
    border-radius: 8px !important;
    overflow: hidden !important;
  }

  .table th,
  .table td {
    padding: 12px 14px !important;
    text-align: left !important;
    color: #e5e7eb !important;
    border: 1px solid rgba(31, 41, 55, 0.6) !important;
  }

  .table th {
    font-weight: 700 !important;
    text-transform: uppercase !important;
    font-size: 0.8rem !important;
    letter-spacing: 0.5px !important;
    color: #9ca3af !important;
    background: rgba(15, 23, 42, 0.8) !important;
    border-bottom: 2px solid rgba(148, 163, 184, 0.3) !important;
  }

  .table thead {
    color: #9ca3af !important;
    border-bottom: 2px solid rgba(148, 163, 184, 0.3) !important;
  }

  .table thead th {
    color: #9ca3af !important;
    background: rgba(15, 23, 42, 0.8) !important;
    font-weight: 700 !important;
  }

  .table tbody {
    color: #e5e7eb !important;
  }

  .table tbody td {
    color: #e5e7eb !important;
    background: transparent !important;
    border-bottom: 1px solid rgba(31, 41, 55, 0.6) !important;
    font-size: 0.85rem !important;
  }

  .table tbody tr {
    background: rgba(15, 23, 42, 0.7) !important;
  }

  .table tbody tr:nth-child(odd) {
    background: rgba(15, 23, 42, 0.85) !important;
  }

  .table tbody tr:nth-child(even) {
    background: rgba(15, 23, 42, 0.95) !important;
  }

  .table tbody tr:hover {
    background: rgba(31, 41, 55, 0.95) !important;
  }

  .table tbody tr:hover td {
    color: #ffffff !important;
    background: rgba(31, 41, 55, 0.95) !important;
  }

  /* Memastikan semua teks di tabel terlihat */
  .panel table.table,
  .panel .table,
  article .table {
    visibility: visible !important;
    opacity: 1 !important;
  }

  .panel table.table th,
  .panel table.table td,
  .panel .table th,
  .panel .table td {
    visibility: visible !important;
    opacity: 1 !important;
  }

  .placeholder {
    margin-top: 8px;
  }

  .placeholder-text {
    color: #9ca3af;
    line-height: 1.6;
    margin: 0;
  }

  .status-badge {
    display: inline-block;
    padding: 4px 10px;
    border-radius: 999px;
    font-size: 0.75rem;
    font-weight: 500;
    background: rgba(31, 41, 55, 0.9);
    color: #9ca3af;
  }

  .status-badge.active {
    background: rgba(34, 197, 94, 0.2);
    color: #22c55e;
    border: 1px solid rgba(34, 197, 94, 0.4);
  }

  @media (max-width: 960px) {
    .layout {
      grid-template-columns: 200px minmax(0, 1fr);
    }

    .brand-text {
      display: flex;
    }

    .menu-item {
      font-size: 0.9rem;
      padding: 8px 10px;
    }

    .stats-row {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    .grid {
      grid-template-columns: minmax(0, 1fr);
    }

    .panel.span-2 {
      grid-column: span 1;
    }
  }

  @media (max-width: 640px) {
    .layout {
      grid-template-columns: minmax(0, 1fr);
    }

    .sidebar {
      display: none;
    }

    .main {
      padding: 14px 12px 18px;
    }

    .topbar h1 {
      font-size: 1.1rem;
    }

    .stats-row {
      grid-template-columns: minmax(0, 1fr);
    }

    .table {
      font-size: 0.75rem;
    }

    .table th,
    .table td {
      padding: 8px 6px;
    }

    .donation-layout {
      overflow-x: auto;
    }

    .table {
      min-width: 600px;
    }
  }
</style>

