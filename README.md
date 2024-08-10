<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Earn Money</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: white;
            color: #333;
        }
        header {
            background-color: #FF0000; /* Red */
            color: white;
            padding: 10px 0;
            text-align: center;
        }
        nav {
            background-color: #FFD700; /* Yellow */
        }
        nav ul {
            list-style: none;
            padding: 0;
            margin: 0;
            display: flex;
            justify-content: center;
        }
        nav ul li {
            margin: 0 15px;
            position: relative;
        }
        nav ul li a {
            color: #FF0000; /* Red */
            text-decoration: none;
            padding: 14px 20px;
            display: block;
        }
        nav ul li a.locked {
            color: grey;
            pointer-events: none;
        }
        nav ul li a:hover {
            background-color: #FFA500; /* Orange */
        }
        nav ul li:hover .drawer {
            display: block;
        }
        .drawer {
            display: none;
            position: absolute;
            top: 50px;
            left: 0;
            background-color: #FFD700; /* Yellow */
            border: 1px solid #FF0000; /* Red */
            padding: 10px;
            width: 200px;
            z-index: 1000;
            box-shadow: 0px 4px 8px rgba(0,0,0,0.1);
        }
        main {
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        section {
            margin-bottom: 40px;
        }
        section h2 {
            color: #FF0000; /* Red */
            border-bottom: 2px solid #FF0000;
            padding-bottom: 10px;
        }
        footer {
            background-color: #FF0000; /* Red */
            color: white;
            text-align: center;
            padding: 20px 0;
        }
        footer h2 {
            margin-top: 0;
        }
        input[type="tel"], input[type="text"] {
            padding: 10px;
            margin: 10px 0;
            width: 80%;
            max-width: 300px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            padding: 10px 20px;
            background-color: #FF0000; /* Red */
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #FF4500; /* Darker Red */
        }
        .modal {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            box-shadow: 0px 4px 8px rgba(0,0,0,0.1);
            z-index: 1000;
            border: 2px solid #FF0000; /* Red */
        }
        .modal.active {
            display: block;
        }
        .modal button {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <header>
        <h1>Earn Money</h1>
    </header>
    <nav>
        <ul>
            <li><a href="#freelance" id="freelance-link" class="locked">Freelance Work</a>
                <div class="drawer">
                    <p>This will be unlocked at Level 5. To advance levels, watch 10 ads.</p>
                </div>
            </li>
            <li><a href="#surveys" id="surveys-link" class="locked">Surveys</a>
                <div class="drawer">
                    <p>This will be unlocked at Level 5. To advance levels, watch 10 ads.</p>
                </div>
            </li>
            <li><a href="#gigs" id="gigs-link" class="locked">Gigs</a>
                <div class="drawer">
                    <p>This will be unlocked at Level 5. To advance levels, watch 10 ads.</p>
                </div>
            </li>
            <li><a href="#selling" id="selling-link" class="locked">Selling Products</a>
                <div class="drawer">
                    <p>This will be unlocked at Level 5. To advance levels, watch 10 ads.</p>
                </div>
            </li>
            <li><a href="#ads" id="ads-link">Watch Ads</a></li>
        </ul>
    </nav>
    <main>
        <section id="freelance">
            <h2>Freelance Work</h2>
            <p>This option will be unlocked at Level 5. To reach the next level, watch 10 ads.</p>
        </section>
        <section id="surveys">
            <h2>Surveys</h2>
            <p>This option will be unlocked at Level 5. To reach the next level, watch 10 ads.</p>
        </section>
        <section id="gigs">
            <h2>Gigs</h2>
            <p>This option will be unlocked at Level 5. To reach the next level, watch 10 ads.</p>
        </section>
        <section id="selling">
            <h2>Selling Products</h2>
            <p>This option will be unlocked at Level 5. To reach the next level, watch 10 ads.</p>
        </section>
        <section id="ads">
            <h2>Earn Money by Watching Ads</h2>
            <p>Watch ads to earn money and unlock other options. Each ad you watch brings you closer to unlocking more earning methods!</p>
            <button onclick="verifyBeforeWatching()">Watch Ad</button>
            <p id="ads-watched">Ads watched: 0/10</p>
        </section>
        <section id="bank-details">
            <h2>Bank Details</h2>
            <p>To receive your earnings, please provide your bank account details below:</p>
            <form>
                <label for="account-number">Bank Account Number:</label><br>
                <input type="text" id="account-number" placeholder="Enter your bank account number"><br>
                <label for="ifsc-code">IFSC Code:</label><br>
                <input type="text" id="ifsc-code" placeholder="Enter IFSC code"><br>
                <label for="phone-number">Phone Number:</label><br>
                <input type="tel" id="phone-number" placeholder="Enter your phone number"><br>
                <button type="submit">Submit Bank Details</button>
            </form>
        </section>
    </main>
    <footer>
        <h2>Get Started</h2>
        <p>Enter your phone number to receive more information:</p>
        <input type="tel" id="footer-phone-number" placeholder="Phone Number">
        <button>Submit</button>
    </footer>

    <div id="verification-modal" class="modal">
        <h2>Verification Required</h2>
        <p>You need to be verified before you can watch ads. Please enter your bank details and phone number first.</p>
        <button onclick="closeModal()">Close</button>
    </div>

    <script>
        let adsWatched = 0;

        function verifyBeforeWatching() {
            const accountNumber = document.getElementById('account-number').value;
            const ifscCode = document.getElementById('ifsc-code').value;
            const phoneNumber = document.getElementById('phone-number').value;

            if (accountNumber && ifscCode && phoneNumber) {
                watchAd();
            } else {
                document.getElementById('verification-modal').classList.add('active');
            }
        }

        function watchAd() {
            adsWatched++;
            document.getElementById('ads-watched').textContent = 'Ads watched: ' + adsWatched + '/10';
            if (adsWatched >= 10) {
                unlockOptions();
            }
        }

        function unlockOptions() {
            const links = document.querySelectorAll('.locked');
            links.forEach(link => {
                link.classList.remove('locked');
                link.innerHTML = link.textContent; // Remove the locked message
            });
        }

        function closeModal() {
            document.getElementById('verification-modal').classList.remove('active');
        }
    </script>
</body>
</html>
