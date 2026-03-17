<?php
session_start();

// ============================================
// KONFIGURASI DATABASE
// ============================================
$host = 'localhost';
$user = 'root';
$pass = '';
$dbname = 'db_keuangan';

try {
    $db = new PDO("mysql:host=$host;dbname=$dbname", $user, $pass);
    $db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch(PDOException $e) {
    die("<div style='color:red; padding:20px;'>Koneksi database gagal: " . $e->getMessage() . "</div>");
}

// ============================================
// FUNGSI HELPER
// ============================================
function rupiah($angka) {
    return 'Rp ' . number_format($angka, 0, ',', '.');
}

function tgl_indonesia($tanggal) {
    $bulan = [1 => 'Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun', 'Jul', 'Agu', 'Sep', 'Okt', 'Nov', 'Des'];
    $tgl = date('d', strtotime($tanggal));
    $bln = $bulan[(int)date('m', strtotime($tanggal))];
    $thn = date('Y', strtotime($tanggal));
    return $tgl . ' ' . $bln . ' ' . $thn;
}

// ============================================
// LOGIN SYSTEM
// ============================================
if (!isset($_SESSION['user_id'])) {
    if (isset($_POST['login'])) {
        $stmt = $db->prepare("SELECT * FROM users WHERE username = ?");
        $stmt->execute([$_POST['username']]);
        $user = $stmt->fetch();
        
        if ($user && password_verify($_POST['password'], $user['password'])) {
            $_SESSION['user_id'] = $user['id'];
            $_SESSION['nama'] = $user['nama_lengkap'];
            header('Location: index.php');
            exit;
        } else {
            $error = "Username atau password salah!";
        }
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
        <title>Login - Aplikasi Keuangan</title>
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
        <style>
            body { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); height: 100vh; display: flex; align-items: center; }
        </style>
    </head>
    <body>
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-md-4">
                    <div class="card shadow-lg">
                        <div class="card-header bg-primary text-white text-center py-3">
                            <h4 class="mb-0">APLIKASI KEUANGAN</h4>
                        </div>
                        <div class="card-body p-4">
                            <?php if (isset($error)): ?>
                                <div class="alert alert-danger"><?php echo $error; ?></div>
                            <?php endif; ?>
                            <form method="POST">
                                <div class="mb-3">
                                    <label class="form-label">Username</label>
                                    <input type="text" name="username" class="form-control" value="admin" required>
                                </div>
                                <div class="mb-3">
                                    <label class="form-label">Password</label>
                                    <input type="password" name="password" class="form-control" value="admin123" required>
                                </div>
                                <button type="submit" name="login" class="btn btn-primary w-100 py-2">MASUK</button>
                            </form>
                            <hr>
                            <div class="text-center text-muted">
                                <small>Username: admin | Password: admin123</small>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </body>
    </html>
    <?php
    exit;
}

// ============================================
// LOGOUT
// ============================================
if (isset($_GET['logout'])) {
    session_destroy();
    header('Location: index.php');
    exit;
}

// ============================================
// PROSES FORM
// ============================================
$user_id = $_SESSION['user_id'];
$message = '';

// TAMBAH TRANSAKSI
if (isset($_POST['tambah_transaksi'])) {
    $stmt = $db->prepare("INSERT INTO transaksi (user_id, kategori_id, tipe, jumlah, deskripsi, tanggal) VALUES (?, ?, ?, ?, ?, ?)");
    $stmt->execute([$user_id, $_POST['kategori_id'] ?: null, $_POST['tipe'], $_POST['jumlah'], $_POST['deskripsi'], $_POST['tanggal']]);
    $message = '<div class="alert alert-success">Transaksi berhasil ditambahkan!</div>';
}

// TAMBAH KATEGORI
if (isset($_POST['tambah_kategori'])) {
    $stmt = $db->prepare("INSERT INTO kategori (user_id, nama_kategori, tipe, icon, warna) VALUES (?, ?, ?, ?, ?)");
    $stmt->execute([$user_id, $_POST['nama_kategori'], $_POST['tipe'], $_POST['icon'], $_POST['warna']]);
    $message = '<div class="alert alert-success">Kategori berhasil ditambahkan!</div>';
}

// TAMBAH TABUNGAN
if (isset($_POST['tambah_tabungan'])) {
    $stmt = $db->prepare("INSERT INTO tabungan (user_id, nama_tabungan, target_amount, current_amount, deadline) VALUES (?, ?, ?, ?, ?)");
    $stmt->execute([$user_id, $_POST['nama_tabungan'], $_POST['target_amount'], $_POST['current_amount'], $_POST['deadline'] ?: null]);
    $message = '<div class="alert alert-success">Tabungan berhasil ditambahkan!</div>';
}

// UPDATE TABUNGAN
if (isset($_POST['update_tabungan'])) {
    $stmt = $db->prepare("UPDATE tabungan SET current_amount = current_amount + ? WHERE id = ? AND user_id = ?");
    $stmt->execute([$_POST['jumlah'], $_POST['id'], $user_id]);
    $message = '<div class="alert alert-success">Tabungan berhasil ditambahkan!</div>';
}

// TAMBAH HUTANG
if (isset($_POST['tambah_hutang'])) {
    $stmt = $db->prepare("INSERT INTO hutang_piutang (user_id, tipe, nama_pihak, jumlah, deskripsi, tanggal_transaksi, tanggal_jatuh_tempo) VALUES (?, ?, ?, ?, ?, ?, ?)");
    $stmt->execute([$user_id, $_POST['tipe'], $_POST['nama_pihak'], $_POST['jumlah'], $_POST['deskripsi'], $_POST['tanggal_transaksi'], $_POST['tanggal_jatuh_tempo'] ?: null]);
    $message = '<div class="alert alert-success">Data berhasil ditambahkan!</div>';
}

// LUNAS HUTANG
if (isset($_POST['lunas_hutang'])) {
    $stmt = $db->prepare("UPDATE hutang_piutang SET status = 'Lunas' WHERE id = ? AND user_id = ?");
    $stmt->execute([$_POST['id'], $user_id]);
    $message = '<div class="alert alert-success">Status berhasil diupdate!</div>';
}

// HAPUS TRANSAKSI
if (isset($_GET['hapus_transaksi'])) {
    $stmt = $db->prepare("DELETE FROM transaksi WHERE id = ? AND user_id = ?");
    $stmt->execute([$_GET['hapus_transaksi'], $user_id]);
    $message = '<div class="alert alert-success">Transaksi berhasil dihapus!</div>';
}

// ============================================
// AMBIL DATA
// ============================================
$menu = isset($_GET['menu']) ? $_GET['menu'] : 'dashboard';

// Data dashboard
$stmt = $db->prepare("SELECT 
    COALESCE(SUM(CASE WHEN tipe = 'Pemasukan' THEN jumlah END), 0) as total_masuk,
    COALESCE(SUM(CASE WHEN tipe = 'Pengeluaran' THEN jumlah END), 0) as total_keluar
    FROM transaksi WHERE user_id = ?");
$stmt->execute([$user_id]);
$saldo = $stmt->fetch();
$total_saldo = $saldo['total_masuk'] - $saldo['total_keluar'];

$stmt = $db->prepare("SELECT 
    COALESCE(SUM(CASE WHEN tipe = 'Pemasukan' THEN jumlah END), 0) as masuk_bulan,
    COALESCE(SUM(CASE WHEN tipe = 'Pengeluaran' THEN jumlah END), 0) as keluar_bulan
    FROM transaksi WHERE user_id = ? AND MONTH(tanggal) = MONTH(CURDATE()) AND YEAR(tanggal) = YEAR(CURDATE())");
$stmt->execute([$user_id]);
$bulan_ini = $stmt->fetch();

// Data transaksi
$stmt = $db->prepare("SELECT t.*, k.nama_kategori, k.warna, k.icon 
    FROM transaksi t 
    LEFT JOIN kategori k ON t.kategori_id = k.id 
    WHERE t.user_id = ? 
    ORDER BY t.tanggal DESC");
$stmt->execute([$user_id]);
$transaksi = $stmt->fetchAll();

// Data kategori
$stmt = $db->prepare("SELECT * FROM kategori WHERE user_id = ? ORDER BY tipe, nama_kategori");
$stmt->execute([$user_id]);
$kategori = $stmt->fetchAll();

// Data tabungan
$stmt = $db->prepare("SELECT * FROM tabungan WHERE user_id = ? ORDER BY created_at DESC");
$stmt->execute([$user_id]);
$tabungan = $stmt->fetchAll();

// Data hutang
$stmt = $db->prepare("SELECT * FROM hutang_piutang WHERE user_id = ? ORDER BY status, tanggal_jatuh_tempo");
$stmt->execute([$user_id]);
$hutang = $stmt->fetchAll();

// Data chart
$chart_labels = [];
$chart_masuk = [];
$chart_keluar = [];
for ($i = 6; $i >= 0; $i--) {
    $tgl = date('Y-m-d', strtotime("-$i days"));
    $chart_labels[] = date('d/m', strtotime($tgl));
    
    $stmt = $db->prepare("SELECT 
        COALESCE(SUM(CASE WHEN tipe = 'Pemasukan' THEN jumlah END), 0) as masuk,
        COALESCE(SUM(CASE WHEN tipe = 'Pengeluaran' THEN jumlah END), 0) as keluar
        FROM transaksi WHERE user_id = ? AND tanggal = ?");
    $stmt->execute([$user_id, $tgl]);
    $data = $stmt->fetch();
    $chart_masuk[] = $data['masuk'];
    $chart_keluar[] = $data['keluar'];
}
?>

<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Keuangan Pribadi</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #f4f6f9; }
        
        .sidebar {
            min-height: 100vh;
            background: linear-gradient(180deg, #2c3e50, #3498db);
            position: fixed;
            width: 260px;
            color: white;
            box-shadow: 2px 0 10px rgba(0,0,0,0.1);
            z-index: 1000;
        }
        
        .sidebar-header {
            padding: 25px 20px;
            text-align: center;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        
        .sidebar-header i {
            font-size: 48px;
            margin-bottom: 10px;
        }
        
        .sidebar-menu {
            padding: 20px 0;
        }
        
        .sidebar-menu a {
            display: block;
            padding: 15px 25px;
            color: rgba(255,255,255,0.8);
            text-decoration: none;
            transition: all 0.3s;
            border-left: 4px solid transparent;
        }
        
        .sidebar-menu a:hover {
            background: rgba(255,255,255,0.15);
            color: white;
            border-left-color: white;
            padding-left: 35px;
        }
        
        .sidebar-menu a.active {
            background: rgba(255,255,255,0.2);
            color: white;
            border-left-color: white;
        }
        
        .sidebar-menu i {
            width: 25px;
            margin-right: 10px;
        }
        
        .content {
            margin-left: 260px;
            padding: 25px;
        }
        
        .card {
            border: none;
            border-radius: 12px;
            box-shadow: 0 3px 15px rgba(0,0,0,0.08);
            margin-bottom: 25px;
            transition: transform 0.3s;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 20px rgba(0,0,0,0.12);
        }
        
        .card-header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-radius: 12px 12px 0 0 !important;
            padding: 15px 20px;
        }
        
        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }
        
        .stat-card {
            padding: 25px;
            border-radius: 12px;
            color: white;
        }
        
        .table thead th {
            background: #f8fafc;
            border-bottom: 2px solid #dee2e6;
            color: #2c3e50;
            font-weight: 600;
        }
        
        .badge-pemasukan { background: #28a745; color: white; padding: 5px 12px; border-radius: 20px; }
        .badge-pengeluaran { background: #dc3545; color: white; padding: 5px 12px; border-radius: 20px; }
        
        @media (max-width: 768px) {
            .sidebar { position: relative; width: 100%; min-height: auto; }
            .content { margin-left: 0; }
        }
    </style>
</head>
<body>
    <!-- SIDEBAR - SEMUA MENU AKTIF -->
    <div class="sidebar">
        <div class="sidebar-header">
            <i class="fas fa-wallet"></i>
            <h5>KeuanganKu</h5>
            <p class="small mb-0"><?php echo $_SESSION['nama']; ?></p>
        </div>
        <div class="sidebar-menu">
            <a href="?menu=dashboard" class="<?php echo $menu == 'dashboard' ? 'active' : ''; ?>">
                <i class="fas fa-home"></i> Dashboard
            </a>
            <a href="?menu=transaksi" class="<?php echo $menu == 'transaksi' ? 'active' : ''; ?>">
                <i class="fas fa-exchange-alt"></i> Transaksi
            </a>
            <a href="?menu=kategori" class="<?php echo $menu == 'kategori' ? 'active' : ''; ?>">
                <i class="fas fa-tags"></i> Kategori
            </a>
            <a href="?menu=tabungan" class="<?php echo $menu == 'tabungan' ? 'active' : ''; ?>">
                <i class="fas fa-piggy-bank"></i> Tabungan
            </a>
            <a href="?menu=hutang" class="<?php echo $menu == 'hutang' ? 'active' : ''; ?>">
                <i class="fas fa-hand-holding-usd"></i> Hutang/Piutang
            </a>
            <a href="?menu=laporan" class="<?php echo $menu == 'laporan' ? 'active' : ''; ?>">
                <i class="fas fa-file-alt"></i> Laporan
            </a>
            <a href="?menu=tambah" class="<?php echo $menu == 'tambah' ? 'active' : ''; ?>">
                <i class="fas fa-plus-circle"></i> Tambah Data
            </a>
            <div style="border-top: 1px solid rgba(255,255,255,0.1); margin: 20px 0;"></div>
            <a href="?logout=1">
                <i class="fas fa-sign-out-alt"></i> Logout
            </a>
        </div>
    </div>

    <!-- MAIN CONTENT -->
    <div class="content">
        <?php echo $message; ?>

        <!-- DASHBOARD -->
        <?php if ($menu == 'dashboard'): ?>
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 class="text-dark">Dashboard</h3>
            <a href="?menu=tambah" class="btn btn-primary">
                <i class="fas fa-plus me-2"></i>Tambah Transaksi
            </a>
        </div>

        <div class="row">
            <div class="col-md-3">
                <div class="card stat-card bg-primary">
                    <div class="d-flex align-items-center">
                        <i class="fas fa-wallet fa-3x me-3"></i>
                        <div>
                            <p class="mb-1 opacity-75">Saldo Total</p>
                            <h4 class="mb-0"><?php echo rupiah($total_saldo); ?></h4>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-3">
                <div class="card stat-card bg-success">
                    <div class="d-flex align-items-center">
                        <i class="fas fa-arrow-up fa-3x me-3"></i>
                        <div>
                            <p class="mb-1 opacity-75">Pemasukan Bulan Ini</p>
                            <h4 class="mb-0"><?php echo rupiah($bulan_ini['masuk_bulan']); ?></h4>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-3">
                <div class="card stat-card bg-danger">
                    <div class="d-flex align-items-center">
                        <i class="fas fa-arrow-down fa-3x me-3"></i>
                        <div>
                            <p class="mb-1 opacity-75">Pengeluaran Bulan Ini</p>
                            <h4 class="mb-0"><?php echo rupiah($bulan_ini['keluar_bulan']); ?></h4>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-3">
                <div class="card stat-card bg-info">
                    <div class="d-flex align-items-center">
                        <i class="fas fa-chart-line fa-3x me-3"></i>
                        <div>
                            <p class="mb-1 opacity-75">Total Transaksi</p>
                            <h4 class="mb-0"><?php echo count($transaksi); ?></h4>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="row">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">
                        <h5 class="mb-0"><i class="fas fa-chart-line me-2"></i>Grafik 7 Hari Terakhir</h5>
                    </div>
                    <div class="card-body">
                        <canvas id="chartDashboard" style="height: 300px;"></canvas>
                    </div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="card">
                    <div class="card-header">
                        <h5 class="mb-0"><i class="fas fa-info-circle me-2"></i>Ringkasan</h5>
                    </div>
                    <div class="card-body">
                        <div class="mb-3">
                            <p class="mb-1">Total Kategori</p>
                            <h5><?php echo count($kategori); ?> Kategori</h5>
                        </div>
                        <div class="mb-3">
                            <p class="mb-1">Total Tabungan</p>
                            <h5><?php echo count($tabungan); ?> Tabungan</h5>
                        </div>
                        <div class="mb-3">
                            <p class="mb-1">Hutang Aktif</p>
                            <h5><?php 
                                $aktif = 0;
                                foreach($hutang as $h) {
                                    if($h['status'] == 'Belum Lunas') $aktif++;
                                }
                                echo $aktif; 
                            ?> Data</h5>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="card">
            <div class="card-header">
                <h5 class="mb-0"><i class="fas fa-history me-2"></i>Transaksi Terbaru</h5>
            </div>
            <div class="card-body">
                <table class="table table-hover">
                    <thead>
                        <tr>
                            <th>Tanggal</th>
                            <th>Kategori</th>
                            <th>Deskripsi</th>
                            <th>Jumlah</th>
                            <th>Tipe</th>
                        </tr>
                    </thead>
                    <tbody>
                        <?php foreach (array_slice($transaksi, 0, 5) as $t): ?>
                        <tr>
                            <td><?php echo tgl_indonesia($t['tanggal']); ?></td>
                            <td>
                                <span class="badge" style="background-color: <?php echo $t['warna'] ?? '#6c757d'; ?>; color: white;">
                                    <i class="<?php echo $t['icon'] ?? 'fas fa-tag'; ?> me-1"></i>
                                    <?php echo $t['nama_kategori'] ?? '-'; ?>
                                </span>
                            </td>
                            <td><?php echo $t['deskripsi'] ?: '-'; ?></td>
                            <td class="<?php echo $t['tipe'] == 'Pemasukan' ? 'text-success' : 'text-danger'; ?> fw-bold">
                                <?php echo rupiah($t['jumlah']); ?>
                            </td>
                            <td>
                                <span class="badge bg-<?php echo $t['tipe'] == 'Pemasukan' ? 'success' : 'danger'; ?>">
                                    <?php echo $t['tipe']; ?>
                                </span>
                            </td>
                        </tr>
                        <?php endforeach; ?>
                    </tbody>
                </table>
            </div>
        </div>

        <!-- TRANSAKSI -->
        <?php elseif ($menu == 'transaksi'): ?>
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 class="text-dark">Semua Transaksi</h3>
            <a href="?menu=tambah" class="btn btn-primary">
                <i class="fas fa-plus me-2"></i>Tambah Transaksi
            </a>
        </div>

        <div class="card">
            <div class="card-body">
                <table class="table table-bordered table-hover">
                    <thead>
                        <tr>
                            <th>Tanggal</th>
                            <th>Kategori</th>
                            <th>Deskripsi</th>
                            <th>Jumlah</th>
                            <th>Tipe</th>
                            <th>Aksi</th>
                        </tr>
                    </thead>
                    <tbody>
                        <?php foreach ($transaksi as $t): ?>
                        <tr>
                            <td><?php echo tgl_indonesia($t['tanggal']); ?></td>
                            <td><?php echo $t['nama_kategori'] ?? '-'; ?></td>
                            <td><?php echo $t['deskripsi'] ?: '-'; ?></td>
                            <td class="<?php echo $t['tipe'] == 'Pemasukan' ? 'text-success' : 'text-danger'; ?> fw-bold">
                                <?php echo rupiah($t['jumlah']); ?>
                            </td>
                            <td>
                                <span class="badge bg-<?php echo $t['tipe'] == 'Pemasukan' ? 'success' : 'danger'; ?>">
                                    <?php echo $t['tipe']; ?>
                                </span>
                            </td>
                            <td>
                                <a href="?hapus_transaksi=<?php echo $t['id']; ?>&menu=transaksi" 
                                   class="btn btn-sm btn-danger"
                                   onclick="return confirm('Yakin ingin menghapus?')">
                                    <i class="fas fa-trash"></i> Hapus
                                </a>
                            </td>
                        </tr>
                        <?php endforeach; ?>
                    </tbody>
                </table>
            </div>
        </div>

        <!-- KATEGORI -->
        <?php elseif ($menu == 'kategori'): ?>
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 class="text-dark">Daftar Kategori</h3>
            <a href="?menu=tambah" class="btn btn-primary">
                <i class="fas fa-plus me-2"></i>Tambah Kategori
            </a>
        </div>

        <div class="row">
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header bg-success text-white">
                        <h5 class="mb-0"><i class="fas fa-arrow-up me-2"></i>Pemasukan</h5>
                    </div>
                    <div class="card-body">
                        <?php foreach ($kategori as $k): ?>
                            <?php if ($k['tipe'] == 'Pemasukan'): ?>
                            <div class="border-bottom py-2 d-flex align-items-center">
                                <span class="badge me-2" style="background-color: <?php echo $k['warna']; ?>; width: 15px; height: 15px; border-radius: 50%;"></span>
                                <i class="<?php echo $k['icon']; ?> me-2"></i>
                                <?php echo $k['nama_kategori']; ?>
                            </div>
                            <?php endif; ?>
                        <?php endforeach; ?>
                    </div>
                </div>
            </div>
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header bg-danger text-white">
                        <h5 class="mb-0"><i class="fas fa-arrow-down me-2"></i>Pengeluaran</h5>
                    </div>
                    <div class="card-body">
                        <?php foreach ($kategori as $k): ?>
                            <?php if ($k['tipe'] == 'Pengeluaran'): ?>
                            <div class="border-bottom py-2 d-flex align-items-center">
                                <span class="badge me-2" style="background-color: <?php echo $k['warna']; ?>; width: 15px; height: 15px; border-radius: 50%;"></span>
                                <i class="<?php echo $k['icon']; ?> me-2"></i>
                                <?php echo $k['nama_kategori']; ?>
                            </div>
                            <?php endif; ?>
                        <?php endforeach; ?>
                    </div>
                </div>
            </div>
        </div>

        <!-- TABUNGAN -->
        <?php elseif ($menu == 'tabungan'): ?>
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 class="text-dark">Tabungan Saya</h3>
            <a href="?menu=tambah" class="btn btn-primary">
                <i class="fas fa-plus me-2"></i>Tambah Tabungan
            </a>
        </div>

        <div class="row">
            <?php if (empty($tabungan)): ?>
                <div class="col-12">
                    <div class="card p-5 text-center">
                        <i class="fas fa-piggy-bank fa-4x text-muted mb-3"></i>
                        <h5>Belum ada tabungan</h5>
                        <a href="?menu=tambah" class="btn btn-primary mt-3">Tambah Tabungan</a>
                    </div>
                </div>
            <?php else: ?>
                <?php foreach ($tabungan as $t): ?>
                <div class="col-md-6 mb-3">
                    <div class="card">
                        <div class="card-body">
                            <h5 class="card-title"><?php echo $t['nama_tabungan']; ?></h5>
                            <div class="progress mb-3" style="height: 30px;">
                                <?php 
                                $persen = $t['target_amount'] > 0 ? min(100, round(($t['current_amount'] / $t['target_amount']) * 100)) : 0;
                                ?>
                                <div class="progress-bar bg-success" style="width: <?php echo $persen; ?>%;">
                                    <?php echo $persen; ?>%
                                </div>
                            </div>
                            <div class="row text-center mb-3">
                                <div class="col-6">
                                    <p class="text-muted mb-1">Terkumpul</p>
                                    <h6 class="fw-bold"><?php echo rupiah($t['current_amount']); ?></h6>
                                </div>
                                <div class="col-6">
                                    <p class="text-muted mb-1">Target</p>
                                    <h6 class="fw-bold"><?php echo rupiah($t['target_amount']); ?></h6>
                                </div>
                            </div>
                            <?php if ($t['deadline']): ?>
                                <p class="text-muted small">Deadline: <?php echo date('d/m/Y', strtotime($t['deadline'])); ?></p>
                            <?php endif; ?>
                            <hr>
                            <form method="POST">
                                <input type="hidden" name="id" value="<?php echo $t['id']; ?>">
                                <div class="input-group">
                                    <input type="number" name="jumlah" class="form-control" placeholder="Jumlah" required>
                                    <button type="submit" name="update_tabungan" class="btn btn-success">Tambah</button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
                <?php endforeach; ?>
            <?php endif; ?>
        </div>

        <!-- HUTANG/PIUTANG -->
        <?php elseif ($menu == 'hutang'): ?>
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h3 class="text-dark">Hutang & Piutang</h3>
            <a href="?menu=tambah" class="btn btn-primary">
                <i class="fas fa-plus me-2"></i>Tambah Data
            </a>
        </div>

        <div class="row">
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header bg-danger text-white">
                        <h5 class="mb-0"><i class="fas fa-arrow-left me-2"></i>Hutang (Anda Berhutang)</h5>
                    </div>
                    <div class="card-body">
                        <?php 
                        $total_hutang = 0;
                        $ada_hutang = false;
                        foreach ($hutang as $h): 
                            if ($h['tipe'] == 'Hutang' && $h['status'] == 'Belum Lunas'): 
                            $ada_hutang = true;
                            $total_hutang += $h['jumlah'];
                        ?>
                        <div class="border-bottom mb-2 pb-2">
                            <div class="d-flex justify-content-between align-items-center">
                                <div>
                                    <strong><?php echo $h['nama_pihak']; ?></strong>
                                    <p class="mb-0 text-muted small"><?php echo $h['deskripsi'] ?: '-'; ?></p>
                                    <?php if ($h['tanggal_jatuh_tempo']): ?>
                                        <small class="text-muted">Jatuh tempo: <?php echo date('d/m/Y', strtotime($h['tanggal_jatuh_tempo'])); ?></small>
                                    <?php endif; ?>
                                </div>
                                <div class="text-end">
                                    <span class="text-danger fw-bold"><?php echo rupiah($h['jumlah']); ?></span>
                                    <form method="POST" class="mt-1">
                                        <input type="hidden" name="id" value="<?php echo $h['id']; ?>">
                                        <button type="submit" name="lunas_hutang" class="btn btn-sm btn-success">Lunas</button>
                                    </form>
                                </div>
                            </div>
                        </div>
                        <?php 
                            endif; 
                        endforeach; 
                        if (!$ada_hutang):
                        ?>
                        <p class="text-muted text-center py-3">Tidak ada hutang</p>
                        <?php endif; ?>
                        <hr>
                        <h6 class="text-end">Total Hutang: <span class="text-danger fw-bold"><?php echo rupiah($total_hutang); ?></span></h6>
                    </div>
                </div>
            </div>
            <div class="col-md-6">
                <div class="card">
                    <div class="card-header bg-success text-white">
                        <h5 class="mb-0"><i class="fas fa-arrow-right me-2"></i>Piutang (Orang Berhutang)</h5>
                    </div>
                    <div class="card-body">
                        <?php 
                        $total_piutang = 0;
                        $ada_piutang = false;
                        foreach ($hutang as $h): 
                            if ($h['tipe'] == 'Piutang' && $h['status'] == 'Belum Lunas'): 
                            $ada_piutang = true;
                            $total_piutang += $h['jumlah'];
                        ?>
                        <div class="border-bottom mb-2 pb-2">
                            <div class="d-flex justify-content-between align-items-center">
                                <div>
                                    <strong><?php echo $h['nama_pihak']; ?></strong>
                                    <p class="mb-0 text-muted small"><?php echo $h['deskripsi'] ?: '-'; ?></p>
                                    <?php if ($h['tanggal_jatuh_tempo']): ?>
                                        <small class="text-muted">Jatuh tempo: <?php echo date('d/m/Y', strtotime($h['tanggal_jatuh_tempo'])); ?></small>
                                    <?php endif; ?>
                                </div>
                                <div class="text-end">
                                    <span class="text-success fw-bold"><?php echo rupiah($h['jumlah']); ?></span>
                                    <form method="POST" class="mt-1">
                                        <input type="hidden" name="id" value="<?php echo $h['id']; ?>">
                                        <button type="submit" name="lunas_hutang" class="btn btn-sm btn-success">Diterima</button>
                                    </form>
                                </div>
                            </div>
                        </div>
                        <?php 
                            endif; 
                        endforeach; 
                        if (!$ada_piutang):
                        ?>
                        <p class="text-muted text-center py-3">Tidak ada piutang</p>
                        <?php endif; ?>
                        <hr>
                        <h6 class="text-end">Total Piutang: <span class="text-success fw-bold"><?php echo rupiah($total_piutang); ?></span></h6>
                    </div>
                </div>
            </div>
        </div>

        <!-- LAPORAN -->
        <?php elseif ($menu == 'laporan'): ?>
        <h3 class="text-dark mb-4">Laporan Keuangan</h3>

        <?php
        $bulan = isset($_GET['bulan']) ? $_GET['bulan'] : date('m');
        $tahun = isset($_GET['tahun']) ? $_GET['tahun'] : date('Y');
        
        $stmt = $db->prepare("SELECT 
            COALESCE(SUM(CASE WHEN tipe = 'Pemasukan' THEN jumlah END), 0) as total_masuk,
            COALESCE(SUM(CASE WHEN tipe = 'Pengeluaran' THEN jumlah END), 0) as total_keluar
            FROM transaksi WHERE user_id = ? AND MONTH(tanggal) = ? AND YEAR(tanggal) = ?");
        $stmt->execute([$user_id, $bulan, $tahun]);
        $lap = $stmt->fetch();
        
        $bulan_arr = ['Januari','Februari','Maret','April','Mei','Juni','Juli','Agustus','September','Oktober','November','Desember'];
        ?>

        <div class="card mb-4">
            <div class="card-body">
                <form method="GET" class="row">
                    <input type="hidden" name="menu" value="laporan">
                    <div class="col-md-4">
                        <select name="bulan" class="form-select">
                            <?php for ($i=1; $i<=12; $i++): ?>
                            <option value="<?php echo $i; ?>" <?php echo $bulan==$i?'selected':''; ?>>
                                <?php echo $bulan_arr[$i-1]; ?>
                            </option>
                            <?php endfor; ?>
                        </select>
                    </div>
                    <div class="col-md-4">
                        <select name="tahun" class="form-select">
                            <?php for ($i=date('Y')-2; $i<=date('Y'); $i++): ?>
                            <option value="<?php echo $i; ?>" <?php echo $tahun==$i?'selected':''; ?>>
                                <?php echo $i; ?>
                            </option>
                            <?php endfor; ?>
                        </select>
                    </div>
                    <div class="col-md-4">
                        <button type="submit" class="btn btn-primary w-100">Tampilkan</button>
                    </div>
                </form>
            </div>
        </div>

        <div class="row mb-4">
            <div class="col-md-4">
                <div class="card bg-success text-white">
                    <div class="card-body text-center">
                        <h6>Total Pemasukan</h6>
                        <h4><?php echo rupiah($lap['total_masuk']); ?></h4>
                    </div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="card bg-danger text-white">
                    <div class="card-body text-center">
                        <h6>Total Pengeluaran</h6>
                        <h4><?php echo rupiah($lap['total_keluar']); ?></h4>
                    </div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="card bg-primary text-white">
                    <div class="card-body text-center">
                        <h6>Saldo</h6>
                        <h4><?php echo rupiah($lap['total_masuk'] - $lap['total_keluar']); ?></h4>
                    </div>
                </div>
            </div>
        </div>

        <!-- TAMBAH DATA -->
        <?php elseif ($menu == 'tambah'): ?>
        <h3 class="text-dark mb-4">Tambah Data</h3>

        <div class="row">
            <div class="col-md-6">
                <!-- Form Tambah Transaksi -->
                <div class="card mb-4">
                    <div class="card-header">
                        <h5 class="mb-0"><i class="fas fa-exchange-alt me-2"></i>Tambah Transaksi</h5>
                    </div>
                    <div class="card-body">
                        <form method="POST">
                            <div class="mb-3">
                                <label class="form-label">Tipe</label>
                                <select name="tipe" class="form-select" required>
                                    <option value="Pemasukan">Pemasukan</option>
                                    <option value="Pengeluaran">Pengeluaran</option>
                                </select>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Kategori</label>
                                <select name="kategori_id" class="form-select">
                                    <option value="">Pilih Kategori</option>
                                    <?php foreach ($kategori as $k): ?>
                                    <option value="<?php echo $k['id']; ?>"><?php echo $k['nama_kategori']; ?></option>
                                    <?php endforeach; ?>
                                </select>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Jumlah (Rp)</label>
                                <input type="number" name="jumlah" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Deskripsi</label>
                                <input type="text" name="deskripsi" class="form-control">
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Tanggal</label>
                                <input type="date" name="tanggal" class="form-control" value="<?php echo date('Y-m-d'); ?>" required>
                            </div>
                            <button type="submit" name="tambah_transaksi" class="btn btn-primary w-100">Simpan</button>
                        </form>
                    </div>
                </div>

                <!-- Form Tambah Kategori -->
                <div class="card mb-4">
                    <div class="card-header">
                        <h5 class="mb-0"><i class="fas fa-tags me-2"></i>Tambah Kategori</h5>
                    </div>
                    <div class="card-body">
                        <form method="POST">
                            <div class="mb-3">
                                <label class="form-label">Nama Kategori</label>
                                <input type="text" name="nama_kategori" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Tipe</label>
                                <select name="tipe" class="form-select" required>
                                    <option value="Pemasukan">Pemasukan</option>
                                    <option value="Pengeluaran">Pengeluaran</option>
                                </select>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Icon</label>
                                <select name="icon" class="form-select">
                                    <option value="fas fa-money-bill-wave">💰 Uang</option>
                                    <option value="fas fa-utensils">🍽️ Makanan</option>
                                    <option value="fas fa-bus">🚗 Transport</option>
                                    <option value="fas fa-shopping-cart">🛒 Belanja</option>
                                </select>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Warna</label>
                                <input type="color" name="warna" class="form-control" value="#3498db">
                            </div>
                            <button type="submit" name="tambah_kategori" class="btn btn-primary w-100">Simpan</button>
                        </form>
                    </div>
                </div>
            </div>

            <div class="col-md-6">
                <!-- Form Tambah Tabungan -->
                <div class="card mb-4">
                    <div class="card-header">
                        <h5 class="mb-0"><i class="fas fa-piggy-bank me-2"></i>Tambah Tabungan</h5>
                    </div>
                    <div class="card-body">
                        <form method="POST">
                            <div class="mb-3">
                                <label class="form-label">Nama Tabungan</label>
                                <input type="text" name="nama_tabungan" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Target (Rp)</label>
                                <input type="number" name="target_amount" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Saldo Awal (Rp)</label>
                                <input type="number" name="current_amount" class="form-control" value="0">
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Deadline (Opsional)</label>
                                <input type="date" name="deadline" class="form-control">
                            </div>
                            <button type="submit" name="tambah_tabungan" class="btn btn-primary w-100">Simpan</button>
                        </form>
                    </div>
                </div>

                <!-- Form Tambah Hutang/Piutang -->
                <div class="card mb-4">
                    <div class="card-header">
                        <h5 class="mb-0"><i class="fas fa-hand-holding-usd me-2"></i>Tambah Hutang/Piutang</h5>
                    </div>
                    <div class="card-body">
                        <form method="POST">
                            <div class="mb-3">
                                <label class="form-label">Tipe</label>
                                <select name="tipe" class="form-select" required>
                                    <option value="Hutang">Hutang (Saya berhutang)</option>
                                    <option value="Piutang">Piutang (Orang berhutang)</option>
                                </select>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Nama Pihak</label>
                                <input type="text" name="nama_pihak" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Jumlah (Rp)</label>
                                <input type="number" name="jumlah" class="form-control" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Deskripsi</label>
                                <input type="text" name="deskripsi" class="form-control">
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Tanggal Transaksi</label>
                                <input type="date" name="tanggal_transaksi" class="form-control" value="<?php echo date('Y-m-d'); ?>" required>
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Tanggal Jatuh Tempo</label>
                                <input type="date" name="tanggal_jatuh_tempo" class="form-control">
                            </div>
                            <button type="submit" name="tambah_hutang" class="btn btn-primary w-100">Simpan</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
        <?php endif; ?>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        <?php if ($menu == 'dashboard'): ?>
        new Chart(document.getElementById('chartDashboard'), {
            type: 'line',
            data: {
                labels: <?php echo json_encode($chart_labels); ?>,
                datasets: [
                    {
                        label: 'Pemasukan',
                        data: <?php echo json_encode($chart_masuk); ?>,
                        borderColor: '#28a745',
                        backgroundColor: 'rgba(40, 167, 69, 0.1)',
                        tension: 0.4,
                        fill: true
                    },
                    {
                        label: 'Pengeluaran',
                        data: <?php echo json_encode($chart_keluar); ?>,
                        borderColor: '#dc3545',
                        backgroundColor: 'rgba(220, 53, 69, 0.1)',
                        tension: 0.4,
                        fill: true
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { position: 'top' }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        ticks: {
                            callback: function(value) {
                                return 'Rp ' + value.toLocaleString('id-ID');
                            }
                        }
                    }
                }
            }
        });
        <?php endif; ?>
    </script>
</body>
</html>