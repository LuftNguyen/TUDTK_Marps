---
marp: true
theme: ucas
paginate: true
math: mathjax
auto scaling: true
---
<!--
_backgroundImage: url("./images/bg1.jpg")
_paginate: false 
-->

<style scoped>
    section {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        background-size: cover; 
    }
    h2.mon-hoc {
        position: absolute;
        top: 25%;
        color: rgb(60, 112, 198);
        font-size: 40px;
    }
    h1.de-tai {
        margin: 0;
        padding: 0;
        font-size: 55px;
        color: white !important; 
    }
    p.nhom {
        position: absolute;
        bottom: 20%;
        color: rgb(60, 112, 198);
        font-size: 30px;
        font-weight: bold;
    }
</style>

<h2 class="mon-hoc">Đồ án môn học Toán Ứng dụng Thống kê </h2>

<h1 class="de-tai">ỨNG DỤNG ĐẠI SỐ TUYẾN TÍNH TRONG HỆ THỐNG GỢI Ý PHIM</h1>

<p class="nhom">Nhóm 15 - 24CTT1</p>

---
<style scoped>
table {
    width: 100%;
    border-collapse: collapse;
    font-size: 24px;
}
th {
    background-color: #3c70c6;
    color: white;
}
td {
    padding: 15px;
}
</style>

### Giới thiệu thành viên

| Họ và tên | MSSV | Nhiệm vụ chính |
| :--- | :---: | :--- |
| **Nguyễn Ngọc Trâm Anh** | 24120019 | Kỹ thuật |
| **Nguyễn Hà Minh Hiền** | 24120046 | Slide |
| **Nguyễn Trọng Hiếu** | 24120050 | Báo cáo |
| **Lý Thảo Nguyên** | 24120105 | Báo cáo |
| **Mai Khắc Hoàng Vũ** | 24120183 | Kỹ thuật|

---
### Nội dung
<style scoped>
    ol {
        counter-reset: list;
        list-style: none;
        padding-left: 100px;
    }
    ol li {
        font-size: 32px;
        margin-bottom: 20px;
        counter-increment: list;
        position: relative;
    }
    ol li::before {
        content: counter(list);
        position: absolute;
        left: -60px;
        background: #3c70c6;
        color: white;
        width: 45px;
        height: 45px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        font-weight: bold;
    }
    strong {
        color: #3c70c6;
    }
</style>

1. **Đặt vấn đề:** Tại sao cần hệ thống gợi ý?
2. **Thực tế:** Các hệ thống gợi ý hiện nay (Netflix, Amazon, Youtube).
3. **Bài toán:** Xác định Input, Output và mô hình dữ liệu.
4. **Ứng dụng Đại số tuyến tính:** Vai trò của Đại số tuyến tính trong bài toán.
5. **Kỹ thuật thực hiện:** Quy trình cài đặt thuật toán và đánh giá.
6. **Phần kết**: Kết luận và hướng phát triển

---
<style scoped>
    section {
        background: linear-gradient(to bottom, 
            white 0%, white 35%, 
            #3c70c6 35%, #3c70c6 65%, 
            white 65%, white 100%);
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 30px;
        margin: 0;
    }
    .container {
        display: flex;
        justify-content: space-around;
        align-items: center;
        height: 100%;
        padding-bottom: 20px; 
    }
    .box {
        color: white;
        text-align: center;
        width: 45%;
    }
    .box h2 {
        font-size: 48px;
        margin: 0;
        padding: 0;
        line-height: 1.2;
    }
    .box p {
        font-size: 22px;
        margin-top: 5px;
        font-weight: normal;
    }
    .arrow {
        font-size: 100px;
        color: white;
        transform: translateY(-5px); 
    }
    .quote {
        position: absolute;
        bottom: 60px;
        width: 85%;
        left: 7.5%;
        font-size: 40px;
        color: #555;
        text-align: center;
    }
</style>

<h1 class="header-title">1) Đặt vấn đề</h1>

<div class="container">
    <div class="box">
        <h2>Sự bùng nổ lựa chọn</h2>
        <p>(Choice Explosion)</p>
    </div>

<div class="arrow">→</div>

<div class="box">
        <h2>Quá tải thông tin</h2>
        <p>(Information Overload)</p>
</div>
</div>

<div class="quote">
    <blockquote>
        Người dùng ngày càng khó khăn trong việc tìm ra nội dung/ sản phẩm thực sự phù hợp với nhu cầu của họ.
    </blockquote>
</div>

---
<style scoped>
    section {
        padding: 0 !important;
        position: relative; 
    }

    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 30px;
        margin: 0;
    }
    
    .image-box {
        position: absolute;
        bottom: 0;
        right: -150px;
        width: 65%; 
        height: 85%; 
        display: flex;
        align-items: flex-end;
    }

    .image-box img {
        width: 100%;
        height: 100%;
        object-fit: cover; 
        border-radius: 20px 0 0 0; 
        box-shadow: -5px -5px 20px rgba(0,0,0,0.1);
    }

    .text-box {
        position: absolute;
        left: 150px;
        top: 40%; 
        width: 25%;
        text-align: left;
    }

    .text-box h3 {
        color: #3c70c6;
        font-size: 40px;
        line-height: 1.3;
        margin-bottom: 10px;
    }

    .text-box p {
        font-size: 24px;
        font-weight: bold;
        color: #555;
    }
</style>

<h1 class="header-title"></h1>

<div class="image-box">

![h:700](./images/amazon.png) 
</div>

<div class="text-box">

### 10,000 kết quả - "bag"
*(Hình 1: Amazon.com)*

</div>

---

<style scoped>
    section {
        padding: 0 !important;
        position: relative; 
    }

    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 30px;
        margin: 0;
    }
    
    .image-box {
        position: absolute;
        bottom: 0;
        right: -250px;
        width: 65%; 
        height: 85%; 
        display: flex;
        align-items: flex-end;
    }

    .image-box img {
        width: 100%;
        height: 100%;
        object-fit: cover; 
        border-radius: 20px 0 0 0; /* Bo góc trên bên trái */
        box-shadow: -5px -5px 20px rgba(0,0,0,0.1);
    }

    .text-box {
        position: absolute;
        left: 150px;
        top: 40%; 
        width: 25%;
        text-align: left;
    }

    .text-box h3 {
        color: #3c70c6;
        font-size: 40px;
        line-height: 1.3;
        margin-bottom: 10px;
    }

    .text-box p {
        font-size: 24px;
        font-weight: bold;
        color: #555;
    }
</style>

<h1 class="header-title"></h1>

<div class="image-box">

![h:700](./images/lazada.png) 
</div>

<div class="text-box">

### 4,794 kết quả - "bag"
*(Hình 2: Lazada.com)*

</div>

---

<style scoped>
    section {
        padding: 0 !important;
        position: relative; 
    }

    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 30px;
        margin: 0;
    }
    
    .image-box {
        position: absolute;
        bottom: 0;
        right: -230px;
        width: 65%; 
        height: 85%; 
        display: flex;
        align-items: flex-end;
    }

    .image-box img {
        width: 100%;
        height: 100%;
        object-fit: cover; 
        border-radius: 20px 0 0 0; 
        box-shadow: -5px -5px 20px rgba(0,0,0,0.1);
    }

    .text-box {
        position: absolute;
        left: 150px;
        top: 40%; 
        width: 25%;
        text-align: left;
    }

    .text-box h3 {
        color: #3c70c6;
        font-size: 40px;
        line-height: 1.3;
        margin-bottom: 10px;
    }

    .text-box p {
        font-size: 24px;
        font-weight: bold;
        color: #555;
    }
</style>

<h1 class="header-title"></h1>

<div class="image-box">

![h:700](./images/taobao.png) 
</div>

<div class="text-box">

### 484,449 kết quả - "bag"
*(Hình 3: taobao.com)*

</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
    }
    .main-container {
        display: flex;
        justify-content: space-between;
        height: 90%;
        margin-top: 20px;
        gap: 30px;
    }
    .column {
        flex: 1;
        padding: 25px;
        border-radius: 15px;
        display: flex; 
        flex-direction: column;
    }
    .solution-box {
        background-color: #eef4ff;
        border-top: 8px solid #3c70c6;
    }
    .challenge-box {
        background-color: #fff5eb;
        border-top: 8px solid #f0ad4e;
        align-items: center; 
    }
    h2 {
        text-align: center;
        margin-bottom: 20px;
        font-size: 35px;
        width: 100%; 
    }
    .solution-box h2 { color: #3c70c6; }
    .challenge-box h2 { color: #8a6d3b; }
    
    ul {
        font-size: 32px;
        line-height: 1.5;
    }
    li { margin-bottom: 12px; }

    .matrix-image {
        max-width: 90%; 
        height: auto;
        margin-top: auto; 
        margin-bottom: 15px;
        border: 1px solid #ccc;
        border-radius: 5px;
    }

    .caption {
        font-size: 25px;
        font-style: italic;
        color: #555;
        text-align: center;
        margin-top: 0;
        margin-bottom: auto; 
    }
</style>

<div class="main-container">

<div class="column solution-box">

## 💡 Giải pháp
**Hệ thống gợi ý** 
- Không hiển thị tất cả
- Chỉ hiển thị lựa chọn người dùng quan tâm
- Hệ thống thu thập "Ma trận đánh giá" (User-Item Matrix) - Ma trận thưa


</div>

<div class="column challenge-box">

## ⚠️ Thách thức

<img src="./images/ratematrix.png" class="matrix-image" alt="Ma trận thưa" />

<p class="caption">(Hình 4: Dựa trên những dữ liệu đã có -->  dự đoán các ô chưa có.)</p>

</div>

</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
        padding-top: 100px;
    }
    
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 30px;
        margin: 0;
    }

    .intro-text {
        font-size: 29px;
        margin-bottom: 20px;
        margin-left: 20px;
    }
    
    .case-studies {
        display: flex;
        justify-content: space-between;
        gap: 20px;
        flex: 1;
    }

    .case-card {
        flex: 1;
        padding: 15px;
        border-radius: 12px;
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: #f9f9f9;
        border: 1px solid #ddd;
        border-top: 5px solid #3c70c6;
    }

    .amazon-card { 
        border-top-color: #ff9900; 
        }
    .youtube-card { 
        border-top-color: #ff0000; 
        }

    .case-card img {
        width: auto;
        margin-bottom: 15px;
        object-fit: contain;
    }

    .amazon-card img {
        max-height: 150px;
        margin-top: 100px;
        width: 90% !important;
    }

    .youtube-img {
        max-height: 580px; 
        width: 90% !important; 
    }

    .case-card p {
        font-size: 22px;
        text-align: justify;
        line-height: 1.5;
        margin-top: auto; 
    }

    .amazon-text {
        margin-top: 20px !important; 
    }

    .img-wrapper {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-bottom: 10px
    }

    .img-caption {
        font-size: 16px; 
        color: #666;    
        font-style: italic;
        margin-top: 5px
    }

    .case-card img {
        margin-bottom: 5px !important; 
    }

</style>

<h1 class="header-title">2) Thực tế</h1>

<ul class="intro-text">
    <li><strong>Đại số tuyến tính</strong> là ngôn ngữ nền tảng của hệ thống gợi ý.</li>
</ul>

<div class="case-studies">
    <div class="case-card amazon-card">
    <div class="img-wrapper">
            <img src="./images/cosine.png" alt="Cosine Similarity Formula" />
            <span class="img-caption">(Hình 5: Công thức Cosine Similarity)</span>
        </div>
        <p class="amazon-text"><b>Amazon:</b> Tiên phong dùng <i>Cosine Similarity</i> để tính sự tương đồng giữa các sản phẩm từ đó tìm ra các sản phẩm "mua cùng nhau".
        <br>
        <br>
        <b>Bài báo:</b> Amazon.com Recommendations: Item-to-Item Collaborative Filtering" - Greg Linden
        </p>
    </div>
    <div class="case-card youtube-card">
    <div class="img-wrapper">
            <img src="./images/youtube.png" class="youtube-img" alt="YouTube Deep Learning Model" />
            <span class="img-caption">(Hình 6: Kiến trúc Neural Network của YouTube)</span>
        </div>
        <p><b>YouTube:</b> Sử dụng lớp <i>Softmax</i> để nhân vector người dùng <b>U</b> với ma trận video <b>V</b>, dự đoán hành vi xem tiếp theo.</p>
    </div>
</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 0 !important;
        background-color: white;
    }
    
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 30px;
        margin: 0;
        z-index: 10;
        text-shadow: 1px 1px 5px rgba(255,255,255,0.8);
    }

    .image-container {
        width: 100%;
        height: 60%; 
        overflow: hidden;
    }

    .image-container img {
        width: 100% !important;
        height: 100% !important; 
    }

    .text-container {
        width: 100%;
        height: 40%;
        padding: 40px 80px;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .text-container p {
        font-size: px; 
        line-height: 1.6;
        color: #333;
        text-align: justify;
        margin: 0;
    }

    strong {
        color: #3c70c6;
    }

    figcaption {
    text-align: center;
    font-size: 18px;
    color: #555;
    font-style: italic;
    margin-top: 10px;
    }
</style>

<div class="image-container">

![w:1920](./images/netflix.png) 
</div>

<figcaption>(Hình 7: BellKor's Pragmatic Chaos tại Netflix Prize năm 2009)</figcaption>

<div class="text-container">

<p>
Áp dụng <strong>phân rã ma trận</strong> bằng kỹ thuật <strong>SVD</strong> chính là thuật toán đã giúp đội <strong>BellKor's Pragmatic Chaos</strong> giành chiến thắng <strong>Netflix Prize</strong> năm 2009 trị giá 1 triệu USD. Thuật toán này đã cải thiện độ chính xác của hệ thống gợi ý Netflix lên hơn 10% và trở thành <strong>kiến trúc nền tảng</strong> cho ngành công nghiệp Hệ thống gợi ý hiện đại.
</p>

</div>

---

<style scoped>
    section {
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: white;
    }

    h1 {
        font-size: 130px; 
        color: #3c70c6; 
        font-weight: bold;
        text-align: center;
    }
</style>

<h1>Hôm nay xem gì?</h1>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
        padding-top: 120px;
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 30px;
        margin: 0;
    }
    .content {
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 30px;
    }
    
    .text-box { 
        width: 40%; 
        margin-top: -100px;
        font-size: 30px
    }
    
    .image-box { 
        width: 55%;
        text-align: center;
        height: 550px; 
        display: flex; 
        justify-content: center;
        align-items: center;
    }
    
    .image-box img {
        height: 100% !important; 
        width: auto !important; 

        object-fit: contain; 
        
        border-radius: 8px;
        box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }
    
    ul { 
        font-size: 30px; 
        line-height: 1.5; 
        }
    .purpose-box {
        background: #f0f4fa;
        padding: 15px;
        border-radius: 10px;
        margin-top: 15px;
    }
</style>
<h1 class="header-title">3) Bài toán, Input, Output </h1>

<div class="content">

<div class="text-box">

- **Bài toán:** Sử dụng SVD để phân rã ma trận tương tác **R** thành hai ma trận thành phần **U** và **V**.

<div class="purpose-box">

**🎯 Mục đích:**
- **Tiết kiệm bộ nhớ** 
- **Xử lý đặc trưng tốt hơn** 

</div>

</div>

<div class="image-box">

![w:500](./images/mf.png)
*(Hình 8: Minh họa phân rã ma trận R thành U và V)*

</div>

</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 30px;
        padding-top: 110px;
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 35px; 
        margin: 0;
    }

    .flow-container {
        display: flex;
        justify-content: space-between;
        gap: 15px;
        margin-top: 20px;
        height: 75%; 
    }

    .column {
        flex: 1;
        padding: 35px 25px; 
        border-radius: 20px;
        background-color: #f8f9fa;
        border-top: 12px solid #3c70c6; 
        box-shadow: 0 6px 15px rgba(0,0,0,0.08);
        display: flex;
        flex-direction: column;
    }

    .train-box { border-top-color: #3c70c6; }
    .input-box { border-top-color: #5bc0de; }
    .output-box { border-top-color: #5cb85c; }

    h2 {
        font-size: 30px;
        margin-bottom: 20px;
        text-align: center;
        color: #3c70c6;
    }

    ul {
        font-size: 26px; 
        line-height: 1.5;
        padding-left: 25px;
    }

    li { margin-bottom: 15px; }

    .note {
        margin-top: auto;
        font-size: 20px; 
        font-style: italic;
        color: #555;
        background: rgba(0,0,0,0.03);
        padding: 15px;
        border-radius: 10px;
        text-align: center;
    }
</style>

<h1 class="header-title">Quy trình: Training, Input & Output</h1>

<div class="flow-container">

<div class="column train-box">
<h2>📥 Training</h2>
        <ul>
            <li><b>UserID</b></li>
            <li><b>MovieID</b></li>
            <li><b>Rating</b>: Đánh giá thực tế</li>
        </ul>
        <div class="note">Dữ liệu lịch sử dùng để học các Latent Factors</div>
    </div>

<div class="column input-box">
        <h2>📥 Input</h2>
        <ul>
            <li><b>UserID</b></li>
            <li><b>MovieID</b>: Tập hợp các phim mà người dùng chưa tương tác.</li>
        </ul>
        <div class="note">Yêu cầu dự đoán dựa trên model đã học</div>
    </div>

<div class="column output-box">
        <h2>📤 Output</h2>
        <ul>
            <li><b>Điểm dự đoán</b>: 1.0 - 5.0 cho từng phim.</li>
            <li><b>Top-n items</b>: Danh sách phim sắp xếp giảm dần theo điểm.</li>
        </ul>
        <div class="note">Kết quả mang tính cá nhân hóa</div>
    </div>

</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
        padding-top: 110px;
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 35px;
        margin: 0;
    }
    .comparison-container {
        display: flex;
        justify-content: space-between;
        gap: 20px;
        margin-top: 20px;
    }
    .box {
        flex: 1;
        padding: 25px;
        border-radius: 15px;
        background: #fdfdfd;
        border: 2px solid #eee;
        display: flex;
        flex-direction: column;
    }
    .svd-box { border-top: 10px solid #d9534f; }
    .sgd-box { border-top: 10px solid #5cb85c; }
    
    h2 { font-size: 32px; margin-bottom: 5px; text-align: center; }
    
    .sub-tag {
        text-align: center;
        font-weight: bold;
        text-transform: uppercase;
        font-size: 38px;
        color: #3c70c6;
        margin-bottom: 15px;
        letter-spacing: 1px;
    }

    .formula-container {
        background: #333;
        color: #fff;
        padding: 15px;
        border-radius: 8px;
        text-align: center;
        margin-bottom: 20px;
        min-height: 80px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    ul { font-size: 29px; line-height: 1.5; padding-left: 20px; flex-grow: 1; }
    li { margin-bottom: 10px; }
    .warning { color: #d9534f; font-weight: bold; }
    .highlight { color: #5cb85c; font-weight: bold; }
</style>

<h1 class="header-title">4) Ứng dụng đại số tuyến tính</h1>

<div class="comparison-container">

<div class="box svd-box">
        <h2>SVD</h2>
        <div class="sub-tag">SVD (Lý thuyết) </div>
        <div class="formula-container">

$$R = U \cdot \Sigma \cdot V^T$$

</div>
        <ul>
            <li class="warning">Chỉ chạy trên ma trận đầy đủ (không có ô trống).</li>
            <li>Không thể tính toán trực tiếp nếu thiếu dữ liệu.</li>
        </ul>
    </div>

<div class="box sgd-box">
        <h2>SGD</h2>
        <div class="sub-tag">SGD (Thực thi)</div>
        <div class="formula-container" style="background: #2c3e50;">

$$R \approx U \cdot V^T$$

</div>
        <ul>
            <li class="highlight">Làm việc trực tiếp với các ô có dữ liệu.</li>
            <li>Sử dụng đạo hàm và sai số để điều chỉnh U và V.</li>
            <li>Tối ưu hóa dần dần để dự đoán các ô còn trống.</li>
        </ul>
    </div>

</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
        padding-top: 110px;
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 35px;
        margin: 0;
    }
    .main-content {
        display: flex;
        flex-direction: column;
        gap: 15px;
        margin-top: 10px;
    }
    .vector-section {
        display: flex;
        justify-content: space-between;
        gap: 20px;
    }
    .card {
        flex: 1;
        background: #f0f4fa;
        padding: 15px 25px;
        border-radius: 12px;
        border-left: 8px solid #3c70c6;
        margin-top: 50px;
        font-size: 32px;
    }
    .math-box {
        background: #333;
        color: #fff;
        padding: 10px;
        border-radius: 15px;
        text-align: center;
        font-size: 35px;
        box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    }
    .decision-box {
        background: #e8f5e9;
        padding: 20px;
        border-radius: 12px;
        border-left: 8px solid #4caf50;
        font-size: 32px;
    }
    .highlight-blue { color: #3c70c6; font-weight: bold; display: block; margin-top: 10px; }
</style>

<h1 class="header-title">Dự đoán bằng Nhân vô hướng (Dot Product)</h1>

<div class="main-content">
    
<div class="vector-section">
        <div class="card">
            <b>👤 User A (Sở thích):</b><br>
            Rất thích Hành động, ghét Lãng mạn
            <span class="highlight-blue">

$\vec{u} = \begin{bmatrix} 0.9 & 0.1 \end{bmatrix}$

</span>
</div>
        <div class="card" style="border-left-color: #ff9800;">
            <b>🎬 Phim "Die Hard":</b><br>
            Nhiều cháy nổ, ít tình cảm
            <span class="highlight-blue">

$\vec{i} = \begin{bmatrix} 0.8 & 0.2 \end{bmatrix}$

</span>
        </div>
    </div>

<div class="math-box">

$$\text{Score} = \vec{u} \cdot \vec{i} = (0.9 \times 0.8) + (0.1 \times 0.2) = 0.74$$

</div>

<div class="decision-box">
        <b>Kết luận:</b> Con số <b>0.74 (74%)</b> đủ cao để nhận diện sự tương quan lớn.
        <br>
        <b>Hành động:</b> Đẩy phim <i>"Die Hard"</i> lên trang chủ cho A
    </div>

</div>

<p style="font-size: 16px; font-style: italic; color: #666;">

* Ngược lại: Với "Titanic" $\vec{i}_{t} = \begin{bmatrix} 0.1 & 0.9 \end{bmatrix} \implies \text{Score} = 0.18$ (Không gợi ý).

</p>



---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
        padding-top: 100px;
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 35px;
        margin: 0;
    }
    .step-container {
        display: flex;
        flex-direction: column;
        gap: 15px;
        margin-top: 10px;
    }
    .step {
        display: flex;
        align-items: flex-start;
        gap: 20px;
        background: #f8f9fa;
        padding: 15px 25px;
        border-radius: 12px;
        border-left: 10px solid #3c70c6;
        box-shadow: 2px 2px 8px rgba(0,0,0,0.05);
    }
    .step-num {
        background: #3c70c6;
        color: white;
        border-radius: 50%;
        width: 40px;
        height: 40px;
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: bold;
        flex-shrink: 0;
        font-size: 20px;
    }
    .step-content { flex-grow: 1; }
    .step-content h3 { margin: 0; color: #333; font-size: 30px; }
    .step-content p { margin: 5px 0; font-size: 25px; color: #555; }
    code {
        background: #e9ecef;
        padding: 2px 6px;
        border-radius: 4px;
        color: #d63384;
        font-family: 'Courier New', Courier, monospace;
        font-size: 25px;
    }
    .proof-box {
        background: #fff3cd;
        border: 1px dashed #856404;
        padding: 10px;
        margin-top: 5px;
        font-weight: bold;
        color: #856404;
        font-size: 17px;
    }
</style>

<h1 class="header-title">5) Kỹ thuật thực hiện </h1>

<div class="step-container">

<div class="step">
        <div class="step-num">1</div>
        <div class="step-content">
            <h3>Chuẩn bị dữ liệu (Dataset)</h3>
            <p>Sử dụng tập dữ liệu <b>MovieLens</b> đã làm sạch từ thư viện Cornac.</p>
            <code>cornac.datasets.movielens.load_feedback()</code>
        </div>
    </div>

<div class="step" style="border-left-color: #5bc0de;">
        <div class="step-num" style="background: #5bc0de;">2</div>
        <div class="step-content">
            <h3>Huấn luyện mô hình (Training)</h3>
            <p>Khởi tạo <code>cornac.models.SVD(k=50)</code> và gọi hàm <code>.fit()</code>.</p>
            <p>Thuật toán tự động tìm ra các ma trận cốt lõi thông qua tối ưu hóa.</p>
        </div>
    </div>

<div class="step" style="border-left-color: #5cb85c;">
        <div class="step-num" style="background: #5cb85c;">3</div>
        <div class="step-content">
            <h3>Toán học và thực nghiệm</h3>
            <p>Trích xuất ma trận <code>U</code> (user_factors) và <code>V</code> (item_factors).</p>
            <p>Tính toán thủ công bằng Numpy: <code>numpy.dot(U[i], V[j])</code></p>
            <div class="proof-box">
                🎯 In kết quả ra màn hình để chứng minh việc dùng trực tiếp dùng toán học để sinh ra kết quả gợi ý
            </div>
        </div>
    </div>

</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
        padding-top: 110px;
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 35px;
        margin: 0;
    }
    .content-wrapper {
        display: flex;
        gap: 30px;
        margin-top: 10px;
    }
    .column {
        flex: 1;
        padding: 20px;
        border-radius: 15px;
    }
    .conclusion-col {
        background: #e3f2fd;
        border-top: 8px solid #1e88e5;
    }
    .future-col {
        background: #f1f8e9;
        border-top: 8px solid #7cb342;
    }
    h2 {
        color: #3c70c6;
        font-size: 28px;
        margin-bottom: 15px;
        display: flex;
        align-items: center;
        gap: 10px;
    }
    ul { font-size: 27px; line-height: 1.6; }
    li { margin-bottom: 10px; }
</style>

<h1 class="header-title">6) Kết luận & Hướng phát triển</h1>

<div class="content-wrapper">

<div class="column conclusion-col">
        <h2>📌 Kết luận</h2>
        <ul>
            <li><b>Đại số tuyến tính</b> là "xương sống" giúp máy tính hiểu được sở thích con người thông qua các con số.</li>
            <li><b>Phân rã ma trận (SVD/SGD)</b> giải quyết triệt để bài toán dữ liệu thưa và gợi ý phim.</li>
            <li>Độ chính xác cao, khả năng mở rộng tốt cho hệ thống thực tế.</li>
        </ul>
    </div>

<div class="column future-col">
        <h2>📌 Hướng phát triển</h2>
        <ul>
            <li><b>Hybrid System:</b> Kết hợp với lọc dựa trên nội dung <b>(Content-based)</b> hoặc lọc Cộng tác <b>(Collaborative Filtering)</b> để giải quyết "Cold Start".</li>
            <li><b>Deep Learning:</b> Ứng dụng <b> Neural Networks</b> (như NCF) để học các đặc trưng phi tuyến tính phức tạp hơn.</li>
            <li><b>Real-time:</b> Tối ưu hóa tốc độ tính toán để gợi ý ngay lập tức theo hành vi thực tế.</li>
        </ul>
    </div>

</div>

---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        padding: 40px;
        padding-top: 110px;
    }
    h1.header-title {
        position: absolute;
        top: 30px;
        left: 60px;
        color: #3c70c6;
        font-size: 35px;
        margin: 0;
    }
    .ref-list {
        margin-top: 10px;
    }
    .ref-item {
        margin-bottom: 20px;
        padding: 15px;
        background: #fdfdfd;
        border-radius: 8px;
        border-left: 5px solid #3c70c6;
        box-shadow: 2px 2px 5px rgba(0,0,0,0.03);
    }
    .ref-item b {
        color: #333;
        font-size: 22px;
    }
    .ref-item p {
        margin: 5px 0 0 0;
        font-size: 18px;
        color: #666;
        line-height: 1.4;
    }
    .link {
        color: #3c70c6;
        font-family: monospace;
        font-size: 16px;
        word-break: break-all;
    }
</style>

<h1 class="header-title">Tài liệu tham khảo (References)</h1>

<div class="ref-list">

<div class="ref-item">
        <b>[1] Matrix Factorization Techniques for Recommender Systems</b>
        <p>Yehuda Koren, Robert Bell, Chris Volinsky. IEEE Computer Society, 2009.</p>
    </div>

<div class="ref-item">
        <b>[2] Cornac: A Comparative Framework for Multimodal Recommender Systems</b>
        <p>Preferred.AI. GitHub Repository & Documentation.</p>
        <div class="link">https://github.com/PreferredAI/cornac</div>
    </div>

<div class="ref-item">
        <b>[3] MovieLens Dataset</b>
        <p>F. Maxwell Harper and Joseph A. Konstan. ACM Transactions on Interactive Intelligent Systems.</p>
        <div class="link">https://grouplens.org/datasets/movielens/</div>
    </div>

<div class="ref-item">
        <b>[4] Amazon.com Recommendations</b>
        <p>Amazon.com Recommendations: Item-to-Item Collaborative Filtering</p>
        <div class="link">https://github.com/wzhe06/Reco-papers/blob/master/Classic%20Recommender%20System/%5BCF%5D%20Amazon%20Recommendations%20Item-to-Item%20Collaborative%20Filtering%20%28Amazon%202003%29.pdf</div>
    </div>

</div>



---
<style scoped>
    section {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        background: linear-gradient(135deg, #3c70c6 0%, #2a4d8a 100%);
        color: white;
    }

    h1 {
        font-size: 80px;
        margin-bottom: 20px;
        border-bottom: 4px solid #ffeb3b;
        padding-bottom: 10px;
    }

    h2 {
        font-size: 35px;
        font-weight: 300;
        margin-bottom: 50px;
        opacity: 0.9;
    }

    .contact-info {
        background: rgba(255, 255, 255, 0.1);
        padding: 20px 40px;
        border-radius: 50px;
        font-size: 22px;
        backdrop-filter: blur(5px);
    }

    .footer-note {
        position: absolute;
        bottom: 40px;
        font-size: 18px;
        opacity: 0.6;
    }
</style>

# CẢM ƠN ĐÃ LẮNG NGHE!
## Q&A - Giải đáp thắc mắc

<div class="contact-info">
    📧 group15@student.hcmus.edu.vn | 💻 github.com/group-15
</div>

<div class="footer-note">
    Bài thuyết trình về Ứng dụng ĐSTT trong hệ thống gợi ý phim
</div>


