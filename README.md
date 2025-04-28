
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RailEase - Train Reservation System</title>
    <style>
        /* Base Styles */
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --success: #2ecc71;
            --danger: #e74c3c;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f5f5;
            color: var(--dark);
            line-height: 1.6;
        }

        /* Header & Navigation */
        header {
            background-color: var(--primary);
            color: white;
            padding: 1rem 2rem;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
        }

        nav ul {
            display: flex;
            list-style: none;
        }

        nav ul li {
            margin-left: 1.5rem;
        }

        nav a {
            color: white;
            text-decoration: none;
            transition: color 0.3s;
        }

        nav a:hover {
            color: var(--secondary);
        }

        /* Hero Section */
        .hero {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), 
                        url('https://images.unsplash.com/photo-1527631746610-bca00a040d60?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80') no-repeat center center/cover;
            height: 70vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            color: white;
            padding: 0 2rem;
        }

        .hero h1 {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
        }

        /* Search Container */
        .search-container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 2rem;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .search-container h2 {
            margin-bottom: 1.5rem;
            color: var(--primary);
        }

        .form-group {
            margin-bottom: 1rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
        }

        .form-group input, 
        .form-group select {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }

        /* Train Results */
        .train-results {
            margin-top: 2rem;
        }

        .train-card {
            background: white;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 1.5rem;
            margin-bottom: 1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .train-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .train-info h3 {
            color: var(--primary);
            margin-bottom: 0.5rem;
        }

        .train-info p {
            color: #666;
            margin-bottom: 0.5rem;
        }

        .train-info .time {
            font-weight: bold;
            color: var(--secondary);
        }

        .train-price {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary);
        }

        .btn {
            display: inline-block;
            background: var(--secondary);
            color: white;
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            transition: background 0.3s;
            text-decoration: none;
        }

        .btn:hover {
            background: #2980b9;
        }

        .btn-book {
            background: var(--success);
        }

        .btn-book:hover {
            background: #27ae60;
        }

        /* Footer */
        footer {
            background: var(--dark);
            color: white;
            text-align: center;
            padding: 1.5rem;
            margin-top: 2rem;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            nav {
                flex-direction: column;
            }
            
            nav ul {
                margin-top: 1rem;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .train-card {
                flex-direction: column;
                text-align: center;
            }
            
            .train-info {
                margin-bottom: 1rem;
            }
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.4);
        }

        .modal-content {
            background-color: #fefefe;
            margin: 10% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 80%;
            max-width: 600px;
            border-radius: 8px;
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }

        .close:hover {
            color: black;
        }

        /* Booking Form */
        .booking-form {
            margin-top: 1rem;
        }

        .booking-form .form-group {
            margin-bottom: 1rem;
        }

        .seat-selection {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            margin: 1rem 0;
        }

        .seat {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #ddd;
            border-radius: 4px;
            cursor: pointer;
        }

        .seat.selected {
            background-color: var(--success);
            color: white;
        }

        .seat.booked {
            background-color: var(--danger);
            color: white;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <header>
        <nav>
            <div class="logo">RailEase</div>
            <ul>
                <li><a href="#" id="homeLink">Home</a></li>
                <li><a href="#" id="searchLink">Book Tickets</a></li>
                <li><a href="#" id="loginLink">Login</a></li>
            </ul>
        </nav>
    </header>
    
    <main id="mainContent">
        <section class="hero">
            <h1>Book Your Train Journey With Ease</h1>
            <a href="#" class="btn" id="searchBtn">Search Trains</a>
        </section>
    </main>
    
    <!-- Login Modal -->
    <div id="loginModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>Login</h2>
            <form id="loginForm">
                <div class="form-group">
                    <label for="loginEmail">Email:</label>
                    <input type="email" id="loginEmail" required>
                </div>
                <div class="form-group">
                    <label for="loginPassword">Password:</label>
                    <input type="password" id="loginPassword" required>
                </div>
                <button type="submit" class="btn">Login</button>
            </form>
            <p>Don't have an account? <a href="#" id="showRegister">Register</a></p>
        </div>
    </div>

    <!-- Register Modal -->
    <div id="registerModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>Register</h2>
            <form id="registerForm">
                <div class="form-group">
                    <label for="regName">Full Name:</label>
                    <input type="text" id="regName" required>
                </div>
                <div class="form-group">
                    <label for="regEmail">Email:</label>
                    <input type="email" id="regEmail" required>
                </div>
                <div class="form-group">
                    <label for="regPassword">Password:</label>
                    <input type="password" id="regPassword" required>
                </div>
                <div class="form-group">
                    <label for="regConfirmPassword">Confirm Password:</label>
                    <input type="password" id="regConfirmPassword" required>
                </div>
                <button type="submit" class="btn">Register</button>
            </form>
        </div>
    </div>

    <!-- Booking Modal -->
    <div id="bookingModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>Book Your Ticket</h2>
            <div id="bookingDetails"></div>
            <form id="bookingForm" class="booking-form">
                <div class="form-group">
                    <label for="passengerName">Passenger Name:</label>
                    <input type="text" id="passengerName" required>
                </div>
                <div class="form-group">
                    <label for="passengerAge">Age:</label>
                    <input type="number" id="passengerAge" required min="1">
                </div>
                <div class="form-group">
                    <label for="passengerGender">Gender:</label>
                    <select id="passengerGender" required>
                        <option value="">Select</option>
                        <option value="male">Male</option>
                        <option value="female">Female</option>
                        <option value="other">Other</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Select Seat:</label>
                    <div class="seat-selection" id="seatSelection">
                        <!-- Seats will be generated by JavaScript -->
                    </div>
                </div>
                <button type="submit" class="btn btn-book">Confirm Booking</button>
            </form>
        </div>
    </div>

    <footer>
        <p>&copy; 2023 RailEase Train Reservation System</p>
    </footer>

    <script>
        // Sample data
        const trains = [
            {
                id: 1,
                name: "Express 101",
                from: "Karachi",
                to: "Lahore",
                departure: "08:00",
                arrival: "20:00",
                date: "2023-12-15",
                seats: 120,
                price: 2500,
                class: "Economy",
                bookedSeats: [1, 5, 10]
            },
            {
                id: 2,
                name: "Business 202",
                from: "Karachi",
                to: "Lahore",
                departure: "12:00",
                arrival: "23:30",
                date: "2023-12-15",
                seats: 50,
                price: 4500,
                class: "Business",
                bookedSeats: [2, 3, 7]
            }
        ];

        // DOM Elements
        const mainContent = document.getElementById('mainContent');
        const searchBtn = document.getElementById('searchBtn');
        const homeLink = document.getElementById('homeLink');
        const searchLink = document.getElementById('searchLink');
        const loginLink = document.getElementById('loginLink');
        const loginModal = document.getElementById('loginModal');
        const registerModal = document.getElementById('registerModal');
        const bookingModal = document.getElementById('bookingModal');
        const closeButtons = document.querySelectorAll('.close');
        const showRegister = document.getElementById('showRegister');
        const loginForm = document.getElementById('loginForm');
        const registerForm = document.getElementById('registerForm');
        const bookingForm = document.getElementById('bookingForm');
        const bookingDetails = document.getElementById('bookingDetails');
        const seatSelection = document.getElementById('seatSelection');

        // Current state
        let currentUser = null;
        let selectedTrain = null;
        let selectedSeat = null;

        // Event Listeners
        searchBtn.addEventListener('click', showSearchPage);
        homeLink.addEventListener('click', showHomePage);
        searchLink.addEventListener('click', showSearchPage);
        loginLink.addEventListener('click', () => loginModal.style.display = 'block');
        showRegister.addEventListener('click', () => {
            loginModal.style.display = 'none';
            registerModal.style.display = 'block';
        });

        closeButtons.forEach(btn => {
            btn.addEventListener('click', function() {
                this.closest('.modal').style.display = 'none';
            });
        });

        window.addEventListener('click', function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.style.display = 'none';
            }
        });

        loginForm.addEventListener('submit', handleLogin);
        registerForm.addEventListener('submit', handleRegister);
        bookingForm.addEventListener('submit', handleBooking);

        // Functions
        function showHomePage() {
            mainContent.innerHTML = `
                <section class="hero">
                    <h1>Book Your Train Journey With Ease</h1>
                    <a href="#" class="btn" id="searchBtn">Search Trains</a>
                </section>
            `;
            document.getElementById('searchBtn').addEventListener('click', showSearchPage);
        }

        function showSearchPage() {
            mainContent.innerHTML = `
                <section class="search-container">
                    <h2>Find Your Train</h2>
                    <form id="searchForm">
                        <div class="form-group">
                            <label for="from">From:</label>
                            <input type="text" id="from" placeholder="Departure station" required>
                        </div>
                        <div class="form-group">
                            <label for="to">To:</label>
                            <input type="text" id="to" placeholder="Arrival station" required>
                        </div>
                        <div class="form-group">
                            <label for="date">Travel Date:</label>
                            <input type="date" id="date" required>
                        </div>
                        <button type="submit" class="btn">Search Trains</button>
                    </form>
                    
                    <div id="results" class="train-results">
                        <!-- Results will be populated by JavaScript -->
                    </div>
                </section>
            `;

            document.getElementById('searchForm').addEventListener('submit', function(e) {
                e.preventDefault();
                const from = document.getElementById('from').value;
                const to = document.getElementById('to').value;
                const date = document.getElementById('date').value;
                searchTrains(from, to, date);
            });
        }

        function searchTrains(from, to, date) {
            const resultsContainer = document.getElementById('results');
            resultsContainer.innerHTML = '';
            
            // Filter trains based on search criteria
            const filteredTrains = trains.filter(train => 
                train.from.toLowerCase().includes(from.toLowerCase()) &&
                train.to.toLowerCase().includes(to.toLowerCase()) &&
                train.date === date
            );
            
            if (filteredTrains.length === 0) {
                resultsContainer.innerHTML = '<p class="no-results">No trains found matching your criteria.</p>';
                return;
            }
            
            filteredTrains.forEach(train => {
                const trainCard = document.createElement('div');
                trainCard.className = 'train-card';
                trainCard.innerHTML = `
                    <div class="train-info">
                        <h3>${train.name}</h3>
                        <p>${train.from} to ${train.to}</p>
                        <p class="time">${train.departure} - ${train.arrival}</p>
                        <p>Class: ${train.class} | Available Seats: ${train.seats - train.bookedSeats.length}</p>
                    </div>
                    <div class="train-actions">
                        <div class="train-price">Rs. ${train.price}</div>
                        <button class="btn btn-book book-btn" data-train-id="${train.id}">Book Now</button>
                    </div>
                `;
                resultsContainer.appendChild(trainCard);
            });

            // Add event listeners to book buttons
            document.querySelectorAll('.book-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const trainId = parseInt(this.getAttribute('data-train-id'));
                    showBookingModal(trainId);
                });
            });
        }

        function showBookingModal(trainId) {
            selectedTrain = trains.find(train => train.id === trainId);
            bookingDetails.innerHTML = `
                <h3>${selectedTrain.name}</h3>
                <p>${selectedTrain.from} to ${selectedTrain.to}</p>
                <p class="time">${selectedTrain.departure} - ${selectedTrain.arrival}</p>
                <p>Class: ${selectedTrain.class} | Price: Rs. ${selectedTrain.price}</p>
            `;

            // Generate seats
            seatSelection.innerHTML = '';
            for (let i = 1; i <= selectedTrain.seats; i++) {
                const seat = document.createElement('div');
                seat.className = 'seat';
                if (selectedTrain.bookedSeats.includes(i)) {
                    seat.classList.add('booked');
                }
                seat.textContent = i;
                seat.addEventListener('click', function() {
                    if (!this.classList.contains('booked')) {
                        document.querySelectorAll('.seat').forEach(s => s.classList.remove('selected'));
                        this.classList.add('selected');
                        selectedSeat = i;
                    }
                });
                seatSelection.appendChild(seat);
            }

            bookingModal.style.display = 'block';
        }

        function handleLogin(e) {
            e.preventDefault();
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            // Simple validation
            if (email && password) {
                currentUser = { email };
                alert('Login successful!');
                loginModal.style.display = 'none';
                loginLink.textContent = 'Logout';
                loginLink.removeEventListener('click', () => loginModal.style.display = 'block');
                loginLink.addEventListener('click', handleLogout);
            } else {
                alert('Please enter both email and password');
            }
        }

        function handleRegister(e) {
            e.preventDefault();
            const name = document.getElementById('regName').value;
            const email = document.getElementById('regEmail').value;
            const password = document.getElementById('regPassword').value;
            const confirmPassword = document.getElementById('regConfirmPassword').value;
            
            if (password !== confirmPassword) {
                alert('Passwords do not match!');
                return;
            }
            
            // In a real app, you would save this to a database
            currentUser = { name, email };
            alert('Registration successful! Please login.');
            registerModal.style.display = 'none';
            loginModal.style.display = 'block';
        }

        function handleLogout() {
            currentUser = null;
            alert('Logged out successfully');
            loginLink.textContent = 'Login';
            loginLink.removeEventListener('click', handleLogout);
            loginLink.addEventListener('click', () => loginModal.style.display = 'block');
        }

        function handleBooking(e) {
            e.preventDefault();
            
            if (!currentUser) {
                alert('Please login to book tickets');
                loginModal.style.display = 'block';
                return;
            }
            
            if (!selectedSeat) {
                alert('Please select a seat');
                return;
            }
            
            const passengerName = document.getElementById('passengerName').value;
            const passengerAge = document.getElementById('passengerAge').value;
            const passengerGender = document.getElementById('passengerGender').value;
            
            // In a real app, you would save this booking to a database
            selectedTrain.bookedSeats.push(selectedSeat);
            alert(`Booking confirmed!\nTrain: ${selectedTrain.name}\nSeat: ${selectedSeat}\nPassenger: ${passengerName}`);
            bookingModal.style.display = 'none';
            
            // Reset form
            bookingForm.reset();
            selectedSeat = null;
        }

        // Initialize the home page
        showHomePage();
    </script>
</body>
</html>