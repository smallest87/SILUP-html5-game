📖 Game Design Document (GDD)
Silup: Operasi Lima Pos
| Versi | Tanggal | Status |
|---|---|---|
| 1.0 Final | 2025-12-02 | GDD Dasar (Siap Implementasi) |
| Platform | HTML5 (Phaser) | Fokus |
1. Visi dan Konsep Inti
1.1 Judul dan Konteks
 * Judul Utama: Silup: Operasi Lima Pos
 * Konsep: Game strategi yang menggunakan diksi lokal "Silup" (Walikan Pulis/Polisi) dan merepresentasikan 5 Pos Polisi sebagai 5 kecamatan di Kota Malang.
 * Target Platform: HTML5 (Web Browser Murni) menggunakan Phaser.
1.2 Genre dan Pitch
 * Genre: Tactical Strategy (Turn-Based Hybrid) / Resource Management.
 * Elevator Pitch (USP): Mengelola 5 Pos Polisi lokal (Malang) di bawah tekanan waktu untuk memecahkan Pathfinding Puzzle (A*) guna menjaga nilai Kenyamanan Warga Global.
1.3 Target Audiens
 * Primer: Casual Gamers (sesi cepat, UI intuitif).
 * Niche: Anggota Kepolisian dan Warga Lokal Malang.
2. Gameplay dan Mekanik Inti
2.1 Loop Game (Alur Inti)
 * Threat Spawn: Maling muncul Out-of-Frame dan memilih Rumah Warga target.
 * Decision Phase: Permainan terjeda (Timer Keputusan 5 detik). Pemain mengalokasikan unit (Klik Pos -> Klik Maling).
 * Chase Initiation: Permainan kembali Real-Time. Polisi (A* Dinamis) mengejar, Maling (A* Statis) bergerak ke target.
 * Resolution (Berhasil): Penangkapan (Tile Collision) -> Mobil Polisi muncul dari Pos Asal -> Maling dan Petugas menghilang ke mobil -> Mobil kembali ke Pos Asal.
 * Scoring & Respawn: Skor dihitung dan Pos menjadi tersedia (Ready) hanya saat Mobil kembali ke Pos Asal. Maling Respawn.
 * Resolution (Gagal): Maling mencapai target. Kenyamanan Warga Global berkurang.
2.2 Kontrol dan Sumber Daya
 * Kontrol: Berbasis Klik/Tap dua langkah (Pilih Pos -> Perintah Maling).
 * Manajemen Sumber Daya: Setiap Pos Polisi hanya memiliki 1 Slot Unit Ready di level awal. Slot menjadi TIDAK TERSEDIA selama pengejaran dan proses kembali mobil.
2.3 Mekanik Kunci A: Pathfinding (A*)
 * Dasar: Grid 30x30 tiles (16x16px).
 * Unit AI: Kedua unit (Polisi/Maling) menggunakan A*. Polisi melakukan recalculate jika perlu; Maling statis (tidak menghindari).
2.4 Kondisi Menang/Kalah (Sesi)
| Kondisi | Mekanik Tegas |
|---|---|
| Menang | Berhasil menangkap semua gelombang Maling yang ditentukan untuk sesi tersebut. |
| Kalah | Nilai Kenyamanan Warga Global mencapai 0 (Global Health). |
| Skor | Skor Poin Tangkapan berfungsi sebagai Mata Uang untuk upgrade Pos Polisi (Meta-Game), bukan penentu kemenangan sesi. |
3. Dunia Game dan Level Design
3.1 Ukuran dan Layout
 * Tile Size: 16x16px.
 * Map Grid: 30x30 tiles (Area Taktis).
 * Viewport: 800x480px (Landscape Mobile).
 * Layout: Peta Taktis (480x480) di kiri; Panel UI Statis (320x480) di kanan.
3.2 Elemen Peta
 * Walkable: Jalan Aspal, Pos Polisi, Rumah Warga.
 * Non-Walkable (Obstacle): Pohon, Tembok. Digunakan untuk memperpanjang rute A*.
 * Spawn: Maling harus spawn di tile jalan yang berada di luar batas visual kamera (Out-of-Frame).
3.3 Penempatan (Berdasarkan Malang/Pizza Frenzy)
 * Pos Polisi: 5 Pos Tersebar Strategis.
 * Rumah Warga: Minimal 15-20 lokasi Terkelompok (Hotspot Risiko Tinggi).
4. Karakter dan Aset
4.1 Unit Bergerak
 * Petugas/Maling: Sprite 16x24px, Animasi Walk N/E/S/W.
 * Mobil Polisi: Sprite terpisah (32x32px), digunakan untuk pick-up dan proses pengembalian skor.
4.2 Aset UI/UX
 * Visual Wajib: Health Bar Kenyamanan Warga Global (Sangat Menonjol), Ikon 5 Pos Polisi, Indikator Rute Maling.
 * Audio Wajib: SFX Jelas (Klik, Tangkap, Gagal) untuk feedback instan.
