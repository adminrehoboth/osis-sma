<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Pemilihan OSIS</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f8fafc;
        }
        
        .backdrop {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 10;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .modal {
            animation: modalFadeIn 0.3s ease-out;
        }
        
        @keyframes modalFadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>
<body>
    <div class="min-h-screen py-12 px-4 sm:px-6 lg:px-8">
        <div class="max-w-4xl mx-auto">
            <div class="text-center mb-12">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/4224b2a9-44ce-4d19-a09e-2e581fea6b08.png" alt="Logo sekolah dengan tulisan OSIS di tengah, latar belakang biru dengan border emas" class="mx-auto mb-4 rounded-full shadow-md">
                <h1 class="text-3xl font-bold text-gray-800 mb-2">PEMILIHAN KETUA OSIS</h1>
                <h2 class="text-xl text-gray-600">Tahun Ajaran 2023/2024</h2>
                <div class="w-full h-1 bg-blue-500 rounded-full mt-4 mx-auto" style="max-width: 200px;"></div>
            </div>
            
            <!-- Form Input Data -->
            <div class="bg-white rounded-xl shadow-md overflow-hidden mb-8">
                <div class="p-6">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Identitas Pemilih</h3>
                    <form id="voterForm" class="space-y-4">
                        <div>
                            <label for="name" class="block text-sm font-medium text-gray-700 mb-1">Nama Lengkap</label>
                            <input type="text" id="name" name="name" required 
                                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                        </div>
                        <div>
                            <label for="kelas" class="block text-sm font-medium text-gray-700 mb-1">Kelas</label>
                            <select id="kelas" name="kelas" required 
                                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                                <option value="">Pilih Kelas</option>
                                <option value="X IPA 1">X IPA 1</option>
                                <option value="X IPA 2">X IPA 2</option>
                                <option value="X IPS 1">X IPS 1</option>
                                <option value="X IPS 2">X IPS 2</option>
                                <option value="XI IPA 1">XI IPA 1</option>
                                <option value="XI IPA 2">XI IPA 2</option>
                                <option value="XI IPS 1">XI IPS 1</option>
                                <option value="XI IPS 2">XI IPS 2</option>
                                <option value="XII IPA 1">XII IPA 1</option>
                                <option value="XII IPA 2">XII IPA 2</option>
                                <option value="XII IPS 1">XII IPS 1</option>
                                <option value="XII IPS 2">XII IPS 2</option>
                            </select>
                        </div>
                        <div>
                            <label for="nis" class="block text-sm font-medium text-gray-700 mb-1">NIS</label>
                            <input type="number" id="nis" name="nis" required 
                                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500">
                        </div>
                        <button type="submit" 
                            class="w-full bg-blue-600 text-white py-2 px-4 rounded-lg hover:bg-blue-700 transition duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50">
                            Lanjutkan Memilih
                        </button>
                    </form>
                </div>
            </div>
            
            <!-- Kandidat Section (Hidden Initially) -->
            <div id="candidatesSection" class="hidden mb-12">
                <div class="text-center mb-8">
                    <h3 class="text-2xl font-bold text-gray-800">CALON KETUA OSIS</h3>
                    <p class="text-gray-600">Silakan pilih salah satu kandidat</p>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6" id="candidatesList">
                    <!-- Kandidat akan diisi oleh JavaScript -->
                </div>
                
                <div class="mt-8 text-center">
                    <button id="submitVote" class="bg-green  -600 text-white py-2 px-6 rounded-lg hover:bg-green-700 transition duration-200 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-opacity-50 font-medium">
                        Submit Pilihan
                    </button>
                </div>
            </div>
            
            <!-- Hasil Pemilihan (Admin) - Hidden by default -->
            <div class="bg-white rounded-xl shadow-md overflow-hidden hidden" id="adminSection">
                <div class="p-6">
                    <h3 class="text-xl font-semibold text-gray-800 mb-4">Hasil Pemilihan</h3>
                    <div class="flex justify-between items-center mb-4">
                        <p class="text-gray-600">Total Suara Masuk: <span id="totalVotes" class="font-semibold text-blue-600">0</span></p>
                        <button id="refreshResults" class="text-sm text-blue-600 hover:text-blue-800">
                            Refresh Hasil
                        </button>
                        <button id="exportResults" class="ml-2 text-sm text-green-600 hover:text-green-800">
                            Export ke Google Sheets
                        </button>
                    </div>
                    <div id="resultsChart" class="w-full h-64">
                        <!-- Chart akan diisi oleh JavaScript -->
                    </div>
                    <div class="mt-4 overflow-x-auto">
                        <table class="min-w-full divide-y divide-gray-200">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kandidat</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Suara</th>
                                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Persentase</th>
                                </tr>
                            </thead>
                            <tbody class="bg-white divide-y divide-gray-200" id="resultsTable">
                                <!-- Hasil akan diisi oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>
                    
                    <div class="mt-6">
                        <h4 class="text-lg font-medium text-gray-800 mb-2">Daftar Pemilih</h4>
                        <div class="overflow-x-auto">
                            <table class="min-w-full divide-y divide-gray-200">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">No</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Nama</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kelas</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">NIS</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Waktu Memilih</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Pilihan</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200" id="votersList">
                                    <!-- Daftar pemilih akan diisi oleh JavaScript -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Admin Login Modal -->
    <div id="loginModal" class="hidden fixed inset-0 bg-gray-600 bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white rounded-lg p-6 w-96">
            <h2 class="text-2xl font-bold mb-4 text-center">Login Admin</h2>
            <form id="adminLoginForm">
                <div class="mb-4">
                    <label class="block text-gray-700 mb-2" for="username">Username</label>
                    <input class="w-full px-3 py-2 border rounded" type="text" id="username" required>
                </div>
                <div class="mb-6">
                    <label class="block text-gray-700 mb-2" for="password">Password</label>
                    <input class="w-full px-3 py-2 border rounded" type="password" id="password" required>
                </div>
                <button type="submit" class="w-full bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-700">
                    Login
                </button>
            </form>
            <button id="closeLoginModal" class="w-full mt-4 bg-gray-300 text-gray-700 py-2 px-4 rounded hover:bg-gray-400">
                Close
            </button>
        </div>
    </div>

    <!-- Admin Panel Link -->
    <div class="fixed bottom-4 right-4">
        <button id="adminPanelBtn" class="bg-gray-800 text-white px-4 py-2 rounded-full shadow-lg hover:bg-gray6'00 transition">
            Admin Panel
        </button>
    </div>

    <script>
        // Data Kandidat
        const candidates = [
            {
                id: 1,
                name: "Ahmad Fauzi",
                kelas: "XI IPA 1",
                vision: "Mewujudkan sekolah yang aktif, kreatif, dan berprestasi",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a993fce3-e1db-4636-8df5-db73bf35757d.png",
                imageAlt: "Siswa berkacamata dengan senyum tulus memakai seragam sekolah, latar belakang warna biru sekolah"
            },
            {
                id: 2,
                name: "Siti Aminah",
                kelas: "XI IPS 2",
                vision: "Sekolah ramah lingkungan dengan kegiatan ekstrakurikuler yang beragam",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a5ef1eee-0ef7-42df-a076-2b860ac8b11c.png",
                imageAlt: "Siswi berhijab dengan tatapan percaya diri, memakai seragam sekolah"

            },
            {
                id: 3,
                name: "Budi Santoso",
                kelas: "XII IPA 1",
                vision: "Meningkatkan prestasi akademik dan non-akademik siswa",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/fe045f52-3325-4051-9a6e-2fa65a576df4.png",
                imageAlt: "Siswa atletik dengan gaya percaya diri memakai seragam olahraga sekolah"
            }
        ];
        
        // Variabel Global
        let currentVoter = {};
        let selectedCandidateId = null;
        const SHEET_URL = "https://docs.google.com/spreadsheets/d/14qOHKpvEJNbhd7PczQO7LzgEFJTc6WyBxtznAWK7v0M/edit#gid=0";
        const SCRIPT_URL = "https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec";
        
        // Inisialisasi localStorage jika belum ada
        if (!localStorage.getItem('votes')) {
            localStorage.setItem('votes', JSON.stringify({}));
        }
        
        if (!localStorage.getItem('voters')) {
            localStorage.setItem('voters', JSON.stringify([]));
        }
        
        if (!localStorage.getItem('voteCount')) {
            const initialVoteCount = {};
            candidates.forEach(candidate => {
                initialVoteCount[candidate.id] = 0;
            });
            localStorage.setItem('voteCount', JSON.stringify(initialVoteCount));
        }
        
        // DOM Elements
        const voterForm = document.getElementById('voterForm');
        const candidatesSection = document.getElementById('candidatesSection');
        const candidatesList = document.getElementById('candidatesList');
        const submitVote = document.getElementById('submitVote');
        const resultsTable = document.getElementById('resultsTable');
        const votersList = document.getElementById('votersList');
        const totalVotes = document.getElementById('totalVotes');
        const refreshResults = document.getElementById('refreshResults');
        
        // Event Listeners
        voterForm.addEventListener('submit', handleVoterSubmit);
        submitVote.addEventListener('click', handleVoteSubmission);
        refreshResults.addEventListener('click', updateResults);
        document.getElementById('exportResults').addEventListener('click', async () => {
            const voters = JSON.parse(localStorage.getItem('voters'));
            try {
                await syncToSheets({ action: 'export', data: voters });
                alert('Data berhasil diekspor ke Google Sheets!');
            } catch (error) {
                alert('Gagal mengekspor data');
            }
        });
        
        // Admin Login Elements
        const adminPanelBtn = document.getElementById('adminPanelBtn');
        const loginModal = document.getElementById('loginModal');
        const adminLoginForm = document.getElementById('adminLoginForm');
        const closeLoginModal = document.getElementById('closeLoginModal');
        const adminSection = document.getElementById('adminSection');
        
        // Admin Login Logic
        adminPanelBtn.addEventListener('click', () => {
            loginModal.classList.remove('hidden');
        });
        
        closeLoginModal.addEventListener('click', () => {
            loginModal.classList.add('hidden');
        });
        
        adminLoginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username === 'admin' && password === 'admin123') {
                loginModal.classList.add('hidden');
                adminSection.classList.remove('hidden');
                window.scrollTo({
                    top: document.getElementById('adminSection').offsetTop,
                    behavior: 'smooth'
                });
            } else {
                alert('Username atau password salah!');
            }
        });
        
        // Tampilkan kandidat saat halaman dimuat
        renderCandidates();
        updateResults();
        
        // Fungsi untuk menampilkan kandidat
        function renderCandidates() {
            candidatesList.innerHTML = '';
            
            candidates.forEach(candidate => {
                const candidateCard = document.createElement('div');
                candidateCard.className = 'bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition duration-200 cursor-pointer';
                candidateCard.id = `candidate-${candidate.id}`;
                candidateCard.addEventListener('click', () => selectCandidate(candidate.id));
                
                candidateCard.innerHTML = `
                    <div class="p-6">
                        <div class="flex flex-col md:flex-row items-center">
                            <div class="mb-4 md:mb-0 md:mr-6">
                                <img src="${candidate.image}" alt="${candidate.imageAlt}" class="w-32 h-32 object-cover rounded-full shadow">
                            </div>
                            <div class="flex-1 text-center md:text-left">
                                <h4 class="text-xl font-semibold text-gray-800">${candidate.name}</h4>
                                <p class="text-gray-600 mb-2">${candidate.kelas}</p>
                                
                                <div class="bg-blue-50 p-3 rounded-lg">
                                    <h5 class="text-sm font-medium text-blue-800 mb-1">Visi:</h5>
                                    <p class="text-sm text-gray-700">${candidate.vision}</p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="mt-4">
                            <div class="flex items-center justify-center">
                                <div class="w-6 h-6 rounded-full border-2 border-gray-300 flex items-center justify-center mr-2 candidate-select"></div>
                                <span class="text-sm text-gray-600">Pilih ${candidate.name}</span>
                            </div>
                        </div>
                    </div>
                `;
                
                candidatesList.appendChild(candidateCard);
            });
        }
        
        // Fungsi untuk memilih kandidat
        function selectCandidate(candidateId) {
            selectedCandidateId = candidateId;
            
            // Reset semua card
            document.querySelectorAll('[id^="candidate-"]').forEach(card => {
                card.classList.remove('ring-2', 'ring-blue-500');
                card.querySelector('.candidate-select').classList.remove('bg-blue-500', 'border-blue-500');
                card.querySelector('.candidate-select').innerHTML = '';
            });
            
            // Highlight card yang dipilih
            const selectedCard = document.getElementById(`candidate-${candidateId}`);
            selectedCard.classList.add('ring-2', 'ring-blue-500');
            const selectIndicator = selectedCard.querySelector('.candidate-select');
            selectIndicator.classList.add('bg-blue-500', 'border-blue-500');
            selectIndicator.innerHTML = '✓';
        }
        
        // Fungsi untuk menangani submit data pemilih
        function handleVoterSubmit(e) {
            e.preventDefault();
            
            const name = document.getElementById('name').value;
            const kelas = document.getElementById('kelas').value;
            const nis = document.getElementById('nis').value;
            
            // Simpan data pemilih sementara
            currentVoter = {
                name,
                kelas,
                nis
            };
            
            // Validasi NIS sudah memilih atau belum
            const voters = JSON.parse(localStorage.getItem('voters'));
            const alreadyVoted = voters.some(voter => voter.nis === nis);
            
            if (alreadyVoted) {
                showModal('Anda sudah menggunakan hak pilih!', 'Satu NIS hanya boleh memilih satu kali.');
                return;
            }
            
            // Sembunyikan form dan tampilkan kandidat
            voterForm.style.display = 'none';
            candidatesSection.classList.remove('hidden');
            
            // Scroll ke bagian kandidat
            candidatesSection.scrollIntoView({ behavior: 'smooth' });
        }
        
        // Fungsi untuk sync data ke Google Sheets
        async function syncToSheets(data) {
            try {
                const response = await fetch(SCRIPT_URL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(data)
                });
                return await response.json();
            } catch (error) {
                console.error('Error syncing to Sheets:', error);
                return null;
            }
        }

        // Fungsi untuk menangani submit pilihan
        async function handleVoteSubmission() {
            if (!selectedCandidateId) {
                showModal('Peringatan', 'Silakan pilih salah satu kandidat terlebih dahulu');
                return;
            }
            
            // Tambahkan vote ke localStorage
            const voteCount = JSON.parse(localStorage.getItem('voteCount'));
            voteCount[selectedCandidateId]++;
            localStorage.setItem('voteCount', JSON.stringify(voteCount));
            
            // Simpan data pemilih
            const voteData = {
                ...currentVoter,
                votedFor: selectedCandidateId,
                timestamp: new Date().toLocaleString()
            };

            const voters = JSON.parse(localStorage.getItem('voters'));
            voters.push(voteData);
            localStorage.setItem('voters', JSON.stringify(voters));
            
            // Sync ke Google Sheets
            await syncToSheets(voteData);
            
            // Tampilkan konfirmasi
            const selectedCandidate = candidates.find(c => c.id === selectedCandidateId);
            
            showModal(
                'Terima Kasih!', 
                `Anda telah berhasil memilih ${selectedCandidate.name} sebagai Ketua OSIS.`,
                true
            );
            
            // Update hasil pemilihan
            updateResults();
            
            // Reset form
            voterForm.reset();
            voterForm.style.display = 'block';
            candidatesSection.classList.add('hidden');
            selectedCandidateId = null;
        }
        
        // Fungsi untuk menampilkan modal
        function showModal(title, message, isSuccess = false) {
            const modal = document.createElement('div');
            modal.className = 'backdrop';
            
            modal.innerHTML = `
                <div class="modal bg-white rounded-lg shadow-xl overflow-hidden w-full max-w-md mx-4">
                    <div class="p-6">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="text-xl font-semibold text-gray-800">${title}</h3>
                            <button class="modal-close text-gray-400 hover:text-gray-500 focus:outline-none">
                                ✕
                            </button>
                        </div>
                        <p class="text-gray-600 mb-6">${message}</p>
                        <button class="w-full ${isSuccess ? 'bg-green-500 hover:bg-green-600' : 'bg-blue-500 hover:bg-blue-600'} text-white py-2 px-4 rounded-lg transition duration-200 focus:outline-none modal-close">
                            Tutup
                        </button>
                    </div>
                </div>
            `;
            
            document.body.appendChild(modal);
            
            // Tutup modal saat diklik
            modal.querySelectorAll('.modal-close').forEach(button => {
                button.addEventListener('click', () => {
                    modal.remove();
                });
            });
        }
        
        // Fungsi untuk update hasil pemilihan
        function updateResults() {
            const voteCount = JSON.parse(localStorage.getItem('voteCount'));
            const voters = JSON.parse(localStorage.getItem('voters'));
            
            // Hitung total vote
            const total = Object.values(voteCount).reduce((sum, count) => sum + count, 0);
            totalVotes.textContent = total;
            
            // Update tabel hasil
            resultsTable.innerHTML = '';
            candidates.forEach(candidate => {
                const count = voteCount[candidate.id] || 0;
                const percentage = total > 0 ? ((count / total) * 100).toFixed(1) : 0;
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td class="px-6 py-4 whitespace-nowrap">
                        <div class="flex items-center">
                            <div class="flex-shrink-0 h-10 w-10">
                                <img src="${candidate.image}" alt="${candidate.imageAlt}" class="h-10 w-10 rounded-full">
                            </div>
                            <div class="ml-4">
                                <div class="text-sm font-medium text-gray-900">${candidate.name}</div>
                                <div class="text-sm text-gray-500">${candidate.kelas}</div>
                            </div>
                        </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                        <div class="text-sm text-gray-900">${count}</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                        <div class="flex items-center">
                            <div class="w-full bg-gray-200 rounded-full h-2.5 mr-2">
                                <div class="bg-blue-600 h-2.5 rounded-full" style="width: ${percentage}%"></div>
                            </div>
                            <div class="text-sm text-gray-600">${percentage}%</div>
                        </div>
                    </td>
                `;
                resultsTable.appendChild(row);
            });
            
            // Update daftar pemilih
            votersList.innerHTML = '';
            voters.forEach((voter, index) => {
                const votedFor = candidates.find(c => c.id === voter.votedFor);
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${index + 1}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${voter.name}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${voter.kelas}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${voter.nis}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${voter.timestamp}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${votedFor ? votedFor.name : 'Tidak valid'}</td>
                `;
                votersList.appendChild(row);
            });
            
            // Draw simple chart (just for visualization)
            drawSimpleChart(voteCount);
        }
        
        // Fungsi untuk menggambar chart sederhana
        function drawSimpleChart(voteCount) {
            const chartContainer = document.getElementById('resultsChart');
            chartContainer.innerHTML = '<canvas id="voteChart"></canvas>';
            
            const ctx = document.getElementById('voteChart').getContext('2d');
            
            // Data untuk chart
            const labels = candidates.map(c => c.name);
            const data = candidates.map(c => voteCount[c.id] || 0);
            const backgroundColors = ['#3B82F6', '#10B981', '#F59E0B'];
            
            // Buat chart
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Jumlah Suara',
                        data: data,
                        backgroundColor: backgroundColors,
                        borderColor: backgroundColors.map(c => c.replace(/^#/, '#').replace(/../g, m => ('0'+Math.round(parseInt(m,16)*0.7).toString(16)).slice(-2))),
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                precision: 0
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            display: false
                        }
                    }
                }
            });
        }
    </script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</body>
</html>

