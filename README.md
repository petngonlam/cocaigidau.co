# banaccre.com
<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "web_ban_acc";

// Kết nối
$conn = new mysqli($servername, $username, $password, $dbname);

<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Web Bán Acc</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header>
        <h1>Website Bán Acc</h1>
        <nav>
            <a href="index.php">Trang chủ</a>
            <a href="nap-the.php">Nạp Thẻ</a>
            <a href="tai-khoan.php">Tài Khoản</a>
        </nav>
    </header>
    <main>
        <h2>Danh sách tài khoản</h2>
        <div class="product-list">
            <!-- Hiển thị danh sách tài khoản từ database -->
            <?php
            include('db/connect.php');
            $result = $conn->query("SELECT * FROM accounts");
            while ($row = $result->fetch_assoc()) {
                echo "<div class='product'>";
                echo "<h3>" . $row['name'] . "</h3>";
                echo "<p>Giá: " . $row['price'] . " VNĐ</p>";
                echo "</div>";
            }
            ?>
        </div>
    </main>
</body>
</html>

<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nạp Thẻ</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <h1>Nạp Thẻ Cào</h1>
    <form action="nap-the-handler.php" method="POST">
        <label for="card_type">Loại thẻ:</label>
        <select name="card_type" id="card_type" required>
            <option value="viettel">Viettel</option>
            <option value="vinaphone">Vinaphone</option>
            <option value="mobifone">Mobifone</option>
        </select>
        <br>
        <label for="card_code">Mã thẻ:</label>
        <input type="text" name="card_code" id="card_code" required>
        <br>
        <label for="serial">Số seri:</label>
        <input type="text" name="serial" id="serial" required>
        <br>
        <button type="submit">Nạp thẻ</button>
    </form>
</body>
</html>

<?php
include('db/connect.php');

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $card_type = $_POST['card_type'];
    $card_code = $_POST['card_code'];
    $serial = $_POST['serial'];

    // Tích hợp API nạp thẻ
    $api_url = "https://example.com/api/nap-the"; // Đổi bằng API thật
    $api_data = [
        "card_type" => $card_type,
        "card_code" => $card_code,
        "serial" => $serial,
        "api_key" => "YOUR_API_KEY"
    ];

    $response = file_get_contents($api_url . '?' . http_build_query($api_data));
    $result = json_decode($response, true);

    if ($result['status'] == 'success') {
        echo "Nạp thẻ thành công! Số tiền cộng: " . $result['amount'] . " VNĐ";
    } else {
        echo "Nạp thẻ thất bại: " . $result['message'];
    }
}
?>
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/your-username/your-repo.git
git push -u origin main
