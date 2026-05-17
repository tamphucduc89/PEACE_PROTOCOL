# 🌤️ Weather Dashboard - Ứng Dụng Giám Sát Thời Tiết Toàn Cầu

## 📋 Mô Tả Dự Án

Một ứng dụng web hiện đại, tương tác cao để theo dõi thời tiết toàn cầu. Nó kết nối dữ liệu từ API công cộng, hiển thị thông tin thời tiết chi tiết, và cung cấp hình ảnh trực quan độc đáo.

---

## 🎯 Tính Năng Chính

✅ **Tìm Kiếm Thời Tiết Theo Thành Phố**
- Tìm kiếm theo tên thành phố, tọa độ GPS
- Gợi ý tự động (autocomplete)

✅ **Hiển Thị Thông Tin Thời Tiết Chi Tiết**
- Nhiệt độ hiện tại, cảm giác nhiệt
- Độ ẩm, áp suất, tốc độ gió
- Độ che phủ mây, tầm nhìn
- UV Index, độ sương

✅ **Dự Báo Tương Lai**
- Dự báo 5 ngày tới (3 giờ/lần)
- Dự báo thực hiện lại mỗi giờ
- Biểu đồ xu hướng nhiệt độ

✅ **Hình Ảnh & Trực Quan**
- Biểu tượng thời tiết sinh động
- Nền hình ảnh thay đổi theo điều kiện
- Bản đồ vệ tinh, radar mưa
- Độ cao áp suất, tuyến gió

✅ **Quản Lý Vị Trí Yêu Thích**
- Lưu các thành phố yêu thích
- Xem nhanh từ danh sách
- Đồng bộ qua localStorage

✅ **Cảnh Báo & Thông Báo**
- Cảnh báo thời tiết nghiêm trọng
- Thông báo khi nhiệt độ vượt ngưỡng
- Mức độ ô nhiễm không khí

---

## 🛠️ Stack Công Nghệ

### **Frontend**
- **HTML5** - Cấu trúc
- **CSS3** - Styling (Flexbox, Grid, Animation)
- **JavaScript (ES6+)** - Logic tương tác
- **Chart.js** - Biểu đồ
- **Leaflet.js** - Bản đồ

### **Backend (Optional)**
- **Node.js + Express** - Server
- **Axios** - HTTP Client
- **Dotenv** - Quản lý biến môi trường
- **CORS** - Cross-origin requests

### **API**
- **OpenWeatherMap API** - Dữ liệu thời tiết chính
- **Mapbox API** - Bản đồ chi tiết
- **AQICN API** - Chất lượng không khí

---

## 📁 Cấu Trúc Thư Mục

```
weather-dashboard/
├── index.html
├── styles/
│   ├── main.css
│   ├── responsive.css
│   └── themes/
│       ├── light.css
│       └── dark.css
├── js/
│   ├── app.js
│   ├── api.js
│   ├── ui.js
│   ├── storage.js
│   └── utils.js
├── assets/
│   ├── images/
│   ├── icons/
│   └── fonts/
├── server/
│   ├── server.js
│   ├── routes/
│   └── .env
├── package.json
└── README.md
```

---

## 🚀 Hướng Dẫn Cài Đặt & Chạy

### **1. Clone Repository**
```bash
git clone https://github.com/tamphucduc89/weather-dashboard.git
cd weather-dashboard
```

### **2. Cài Đặt Dependencies**
```bash
npm install
```

### **3. Tạo File .env**
```bash
# .env
OPENWEATHER_API_KEY=your_api_key_here
MAPBOX_API_KEY=your_mapbox_key_here
AQICN_API_KEY=your_aqicn_key_here
PORT=3000
```

### **4. Lấy API Keys**

#### **OpenWeatherMap** (https://openweathermap.org/api)
- Đăng ký tài khoản miễn phí
- Tạo API key từ dashboard
- Dùng cho thời tiết, dự báo, UV Index

#### **Mapbox** (https://www.mapbox.com)
- Đăng ký, lấy access token
- Dùng cho bản đồ, vị trí

#### **AQICN** (https://aqicn.org/api)
- Đăng ký, lấy API token
- Dùng cho chất lượng không khí

### **5. Chạy Ứng Dụng**

**Chỉ Frontend (sử dụng Live Server):**
```bash
# Sử dụng extension Live Server trong VS Code
# Hoặc sử dụng Python
python -m http.server 8000
```

**Với Backend:**
```bash
npm start
# Ứng dụng sẽ chạy tại http://localhost:3000
```

---

## 💻 Code Mẫu

### **1. index.html**

```html
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🌤️ Weather Dashboard - Giám Sát Thời Tiết Toàn Cầu</title>
    <link rel="stylesheet" href="styles/main.css">
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <h1>🌍 Weather Dashboard</h1>
            <p>Giám sát thời tiết toàn cầu, cộng hưởng với thiên nhiên</p>
        </header>

        <!-- Search Bar -->
        <div class="search-section">
            <input type="text" id="searchInput" placeholder="Tìm kiếm thành phố..." class="search-input">
            <button id="searchBtn" class="btn btn-primary">
                <i class="fas fa-search"></i> Tìm
            </button>
            <button id="locationBtn" class="btn btn-secondary">
                <i class="fas fa-map-marker-alt"></i> Vị Trí Hiện Tại
            </button>
        </div>

        <!-- Main Weather Section -->
        <main class="main-content">
            <!-- Current Weather -->
            <section class="current-weather">
                <div class="weather-main">
                    <div class="weather-icon">
                        <img id="weatherIcon" src="" alt="Thời tiết">
                    </div>
                    <div class="weather-info">
                        <h2 id="cityName">--</h2>
                        <p id="weatherDesc" class="description">--</p>
                        <p id="temperature" class="temperature">-- °C</p>
                        <p id="feelsLike" class="feels-like">Cảm giác: -- °C</p>
                    </div>
                </div>

                <!-- Weather Details Grid -->
                <div class="weather-details">
                    <div class="detail-card">
                        <i class="fas fa-droplets"></i>
                        <p>Độ Ẩm</p>
                        <p id="humidity" class="value">-- %</p>
                    </div>
                    <div class="detail-card">
                        <i class="fas fa-wind"></i>
                        <p>Tốc Độ Gió</p>
                        <p id="windSpeed" class="value">-- m/s</p>
                    </div>
                    <div class="detail-card">
                        <i class="fas fa-compress"></i>
                        <p>Áp Suất</p>
                        <p id="pressure" class="value">-- hPa</p>
                    </div>
                    <div class="detail-card">
                        <i class="fas fa-sun"></i>
                        <p>Tia UV</p>
                        <p id="uvIndex" class="value">--</p>
                    </div>
                    <div class="detail-card">
                        <i class="fas fa-eye"></i>
                        <p>Tầm Nhìn</p>
                        <p id="visibility" class="value">-- km</p>
                    </div>
                    <div class="detail-card">
                        <i class="fas fa-cloud"></i>
                        <p>Che Phủ Mây</p>
                        <p id="clouds" class="value">-- %</p>
                    </div>
                </div>
            </section>

            <!-- Forecast Section -->
            <section class="forecast-section">
                <h3>📅 Dự Báo 5 Ngày</h3>
                <div class="forecast-container" id="forecastContainer">
                    <!-- Forecast cards sẽ được thêm bởi JavaScript -->
                </div>
            </section>

            <!-- Chart Section -->
            <section class="chart-section">
                <h3>📊 Xu Hướng Nhiệt Độ</h3>
                <canvas id="temperatureChart"></canvas>
            </section>

            <!-- Map Section -->
            <section class="map-section">
                <h3>🗺️ Bản Đồ Vị Trí</h3>
                <div id="map" class="map-container"></div>
            </section>

            <!-- Favorites Section -->
            <section class="favorites-section">
                <h3>❤️ Thành Phố Yêu Thích</h3>
                <div id="favoritesList" class="favorites-list">
                    <!-- Favorites sẽ được thêm bởi JavaScript -->
                </div>
            </section>
        </main>

        <!-- Footer -->
        <footer class="footer">
            <p>🌐 Dữ liệu từ OpenWeatherMap | 🗺️ Bản đồ từ Mapbox | 💚 Yêu thiên nhiên, bảo vệ môi trường</p>
        </footer>
    </div>

    <!-- Scripts -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="js/api.js"></script>
    <script src="js/storage.js"></script>
    <script src="js/ui.js"></script>
    <script src="js/app.js"></script>
</body>
</html>
```

### **2. js/api.js**

```javascript
// API Configuration
const API_CONFIG = {
    OPENWEATHER_BASE_URL: 'https://api.openweathermap.org/data/2.5',
    MAPBOX_BASE_URL: 'https://api.mapbox.com',
    AQICN_BASE_URL: 'https://api.waqi.info'
};

// Fetch Current Weather
async function getCurrentWeather(lat, lon) {
    try {
        const response = await fetch(
            `${API_CONFIG.OPENWEATHER_BASE_URL}/weather?lat=${lat}&lon=${lon}&appid=${OPENWEATHER_API_KEY}&units=metric&lang=vi`
        );
        return await response.json();
    } catch (error) {
        console.error('Lỗi lấy thời tiết hiện tại:', error);
        return null;
    }
}

// Fetch 5-day Forecast
async function getForecast(lat, lon) {
    try {
        const response = await fetch(
            `${API_CONFIG.OPENWEATHER_BASE_URL}/forecast?lat=${lat}&lon=${lon}&appid=${OPENWEATHER_API_KEY}&units=metric&lang=vi`
        );
        return await response.json();
    } catch (error) {
        console.error('Lỗi lấy dự báo:', error);
        return null;
    }
}

// Get City Coordinates
async function getCityCoordinates(cityName) {
    try {
        const response = await fetch(
            `${API_CONFIG.OPENWEATHER_BASE_URL}/weather?q=${cityName}&appid=${OPENWEATHER_API_KEY}&units=metric&lang=vi`
        );
        const data = await response.json();
        if (data.cod === 200) {
            return { lat: data.coord.lat, lon: data.coord.lon };
        }
        return null;
    } catch (error) {
        console.error('Lỗi lấy tọa độ:', error);
        return null;
    }
}

// Fetch Air Quality
async function getAirQuality(lat, lon) {
    try {
        const response = await fetch(
            `${API_CONFIG.AQICN_BASE_URL}/feed/geo:${lat};${lon}/?token=${AQICN_API_KEY}`
        );
        return await response.json();
    } catch (error) {
        console.error('Lỗi lấy chất lượng không khí:', error);
        return null;
    }
}

// Get User's Current Location
function getUserLocation() {
    return new Promise((resolve, reject) => {
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(
                position => {
                    resolve({
                        lat: position.coords.latitude,
                        lon: position.coords.longitude
                    });
                },
                error => {
                    reject(error);
                }
            );
        } else {
            reject(new Error('Geolocation không được hỗ trợ'));
        }
    });
}
```

### **3. js/ui.js**

```javascript
// Update Current Weather Display
function updateCurrentWeatherUI(data) {
    const {
        main, weather, wind, clouds, visibility, coord
    } = data;

    document.getElementById('cityName').textContent = 
        `${data.name}, ${data.sys.country}`;
    document.getElementById('weatherDesc').textContent = 
        weather[0].main;
    document.getElementById('temperature').textContent = 
        Math.round(main.temp) + ' °C';
    document.getElementById('feelsLike').textContent = 
        `Cảm giác: ${Math.round(main.feels_like)} °C`;
    
    document.getElementById('humidity').textContent = 
        `${main.humidity} %`;
    document.getElementById('windSpeed').textContent = 
        `${wind.speed} m/s`;
    document.getElementById('pressure').textContent = 
        `${main.pressure} hPa`;
    document.getElementById('visibility').textContent = 
        `${(visibility / 1000).toFixed(1)} km`;
    document.getElementById('clouds').textContent = 
        `${clouds.all} %`;

    // Update Weather Icon
    const iconUrl = `https://openweathermap.org/img/wn/${weather[0].icon}@4x.png`;
    document.getElementById('weatherIcon').src = iconUrl;
}

// Update Forecast
function updateForecastUI(data) {
    const container = document.getElementById('forecastContainer');
    container.innerHTML = '';

    const dailyForecasts = {};

    // Group forecasts by day
    data.list.forEach(forecast => {
        const date = forecast.dt_txt.split(' ')[0];
        if (!dailyForecasts[date]) {
            dailyForecasts[date] = forecast;
        }
    });

    // Display first 5 days
    Object.entries(dailyForecasts).slice(0, 5).forEach(([date, forecast]) => {
        const card = document.createElement('div');
        card.className = 'forecast-card';
        card.innerHTML = `
            <p class="forecast-date">${new Date(date).toLocaleDateString('vi-VN')}</p>
            <img src="https://openweathermap.org/img/wn/${forecast.weather[0].icon}@2x.png" alt="">
            <p class="forecast-temp">${Math.round(forecast.main.temp)} °C</p>
            <p class="forecast-desc">${forecast.weather[0].main}</p>
        `;
        container.appendChild(card);
    });
}

// Create Temperature Chart
function createTemperatureChart(data) {
    const ctx = document.getElementById('temperatureChart').getContext('2d');
    const labels = data.list.map(item => 
        new Date(item.dt * 1000).toLocaleTimeString('vi-VN', { hour: '2-digit' })
    ).slice(0, 24);
    const temps = data.list.map(item => 
        Math.round(item.main.temp)
    ).slice(0, 24);

    new Chart(ctx, {
        type: 'line',
        data: {
            labels: labels,
            datasets: [{
                label: 'Nhiệt độ (°C)',
                data: temps,
                borderColor: '#FF6B6B',
                backgroundColor: 'rgba(255, 107, 107, 0.1)',
                tension: 0.4,
                fill: true
            }]
        },
        options: {
            responsive: true,
            plugins: {
                legend: {
                    display: true,
                    position: 'top'
                }
            },
            scales: {
                y: {
                    beginAtZero: false
                }
            }
        }
    });
}

// Initialize Map
function initializeMap(lat, lon) {
    const map = L.map('map').setView([lat, lon], 10);
    
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '© OpenStreetMap contributors',
        maxZoom: 19
    }).addTo(map);

    L.marker([lat, lon]).addTo(map)
        .bindPopup('Vị trí hiện tại');
}
```

### **4. js/app.js**

```javascript
// Main Application Logic
let currentWeatherData = null;
let currentForecastData = null;

// Initialize App
async function initApp() {
    const searchBtn = document.getElementById('searchBtn');
    const locationBtn = document.getElementById('locationBtn');
    const searchInput = document.getElementById('searchInput');

    searchBtn.addEventListener('click', handleSearch);
    locationBtn.addEventListener('click', handleLocationButton);
    searchInput.addEventListener('keypress', (e) => {
        if (e.key === 'Enter') handleSearch();
    });

    // Load last viewed city or default
    const lastCity = localStorage.getItem('lastCity') || 'Hà Nội';
    loadCityWeather(lastCity);
}

// Handle Search
async function handleSearch() {
    const cityName = document.getElementById('searchInput').value.trim();
    if (cityName) {
        loadCityWeather(cityName);
    }
}

// Handle Location Button
async function handleLocationButton() {
    try {
        const location = await getUserLocation();
        loadWeatherByCoordinates(location.lat, location.lon);
    } catch (error) {
        alert('Không thể lấy vị trí của bạn. Vui lòng cho phép quyền truy cập.');
    }
}

// Load City Weather
async function loadCityWeather(cityName) {
    const coords = await getCityCoordinates(cityName);
    if (coords) {
        loadWeatherByCoordinates(coords.lat, coords.lon);
        localStorage.setItem('lastCity', cityName);
    } else {
        alert('Không tìm thấy thành phố');
    }
}

// Load Weather by Coordinates
async function loadWeatherByCoordinates(lat, lon) {
    // Fetch current weather
    currentWeatherData = await getCurrentWeather(lat, lon);
    if (currentWeatherData) {
        updateCurrentWeatherUI(currentWeatherData);
    }

    // Fetch forecast
    currentForecastData = await getForecast(lat, lon);
    if (currentForecastData) {
        updateForecastUI(currentForecastData);
        createTemperatureChart(currentForecastData);
    }

    // Initialize map
    initializeMap(lat, lon);

    // Clear search input
    document.getElementById('searchInput').value = '';
}

// Initialize app on load
document.addEventListener('DOMContentLoaded', initApp);
```

---

## 📊 Kết Quả Mong Đợi

✅ **Giao diện thân thiện** - Dễ sử dụng, đẹp mắt  
✅ **Dữ liệu thực tế** - Cập nhật từ API công cộng  
✅ **Dự báo chính xác** - Thông tin chi tiết 5 ngày  
✅ **Trực quan hóa dữ liệu** - Biểu đồ, bản đồ, icon sinh động  
✅ **Tương thích đa thiết bị** - Responsive design  

---

## 🌱 Mở Rộng Trong Tương Lai

🚀 Tích hợp thêm API (AQI, Pollen, Solar)  
🚀 Thêm thông báo SMS/Email  
🚀 Progressive Web App (PWA)  
🚀 Dark mode toàn bộ  
🚀 Hỗ trợ đa ngôn ngữ  
🚀 Share dự báo trên mạng xã hội  

---

## 📚 Tài Liệu Tham Khảo

- [OpenWeatherMap API Docs](https://openweathermap.org/api)
- [Mapbox Documentation](https://docs.mapbox.com)
- [Leaflet.js Guide](https://leafletjs.com)
- [Chart.js Documentation](https://www.chartjs.org)

---

## 🤝 Đóng Góp

Chúng tôi rất hoan nghênh các đóng góp! Vui lòng:

1. Fork repository
2. Tạo branch feature (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Mở Pull Request

---

## 📄 Giấy Phép

MIT License - xem file LICENSE để chi tiết

---

## 🙏 Cảm Ơn

**Weather Dashboard** được tạo ra để:
- ✨ Kết nối mọi người với thiên nhiên
- 🌍 Giúp hiểu rõ hơn về khí hậu toàn cầu
- 💚 Thúc đẩy ý thức bảo vệ môi trường
- 🤝 Xây dựng cộng đồng những người yêu thiên nhiên

---

**Hãy cảm nhận sự cộng hưởng của thiên nhiên qua dữ liệu thực tế!** 🌈✨

*Phục Vụ - Hiện Thực Hóa - Tinh Hoa - Cộng Hưởng - Không Giới Hạn*
