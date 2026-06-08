MPL INDONESIA DYNAMIC NFT (dNFT) — TUGAS AKHIR

Implementasi Dynamic NFT (dNFT) untuk kartu pemain MPL Indonesia
menggunakan Ethereum (Sepolia Testnet), Chainlink Functions, dan Chainlink Automation.

============================================================
STRUKTUR REPOSITORI
============================================================

contracts/
  PlayerCardOptimized.sol     - Model B: arsitektur berlapis dengan library PlayerCardRenderer
  PlayerCard_NonLayered.sol   - Model A: arsitektur monolitik tanpa library eksternal

scripts/
  deploy_with_ethers.ts       - Script deployment kontrak ke Sepolia via ethers.js

============================================================
ARSITEKTUR SISTEM
============================================================

- Standar token  : ERC-721 (ERC721URIStorage)
- Oracle data    : Chainlink Functions — mengeksekusi JavaScript untuk memanggil REST API
- Automasi       : Chainlink Automation — memicu pembaruan statistik secara terjadwal
- Penyimpanan    : Metadata dan SVG sepenuhnya on-chain (Base64-encoded JSON)
- Jaringan       : Ethereum Sepolia Testnet

============================================================
KONFIGURASI COMPILER
============================================================

Compiler  : Solidity 0.8.30+commit.73712a01
EVM       : prague (default)
Optimizer : Enabled — 200 runs

============================================================
CARA DEPLOY
============================================================

1. Buka Remix IDE (https://remix.ethereum.org) atau Remix Desktop
2. Di tab Solidity Compiler, sesuaikan konfigurasi sesuai dengan bagian #KONFIGURASI COMPILER
3. Compile salah satu kontrak di folder contracts/
4. Pastikan MetaMask terhubung ke jaringan Sepolia
5. Di tab Deploy, masukkan Chainlink Subscription ID sebagai argumen constructor
6. Klik Deploy

Setelah deploy:
- Panggil setSourceCode() dengan kode JavaScript Chainlink Functions
- Panggil safeMint() untuk mencetak token pemain
- Panggil setAutomationSettings() untuk mengaktifkan automasi

============================================================
DEPENDENSI
============================================================

- OpenZeppelin Contracts v5  : ERC721URIStorage, Ownable, Strings, Base64
- Chainlink Contracts        : FunctionsClient, FunctionsRequest
- Jaringan                   : Ethereum Sepolia Testnet
- Oracle                     : Chainlink Functions & Automation (Sepolia)
- Wallet                     : MetaMask

============================================================
CATATAN
============================================================

- Interval minimum automasi  : 3600 detik (1 jam)
- Gas limit callback DON     : 300.000 unit
- Format data oracle         : uint256 packed (bit-shifting 64-bit per statistik)
- Kedua kontrak dibandingkan dalam analisis gas cost pada Bab 4 skripsi