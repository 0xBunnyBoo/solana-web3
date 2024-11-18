my-crypto-website/
├── index.html
├── styles.css
└── script.js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crypto Wallet Connection</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Connect to Crypto Wallet</h1>
    <button id="connectEthereumButton">Connect Ethereum Wallet</button>
    <p id="ethereumAccount">Not connected</p>
    
    <button id="connectSolanaButton">Connect Solana Wallet</button>
    <p id="solanaAccount">Not connected</p>

    <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@solana/web3.js@latest/lib/index.iife.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin-top: 50px;
}

h1 {
    color: #333;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    margin: 10px;
}

p {
    margin-top: 20px;
    font-size: 18px;
    color: #666;
}
document.getElementById('connectEthereumButton').addEventListener('click', async () => {
    if (window.ethereum) {
        try {
            // درخواست دسترسی به حساب‌های کاربری
            const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' });
            // اتصال به حساب کاربری
            document.getElementById('ethereumAccount').textContent = `Connected: ${accounts[0]}`;
        } catch (error) {
            console.error('User denied account access', error);
        }
    } else {
        console.error('No Ethereum provider found. Install MetaMask.');
    }
});

document.getElementById('connectSolanaButton').addEventListener('click', async () => {
    try {
        const provider = window.solana;
        if (provider && provider.isPhantom) {
            // درخواست دسترسی به حساب‌های کاربری
            const resp = await provider.connect();
            // اتصال به حساب کاربری
            document.getElementById('solanaAccount').textContent = `Connected: ${resp.publicKey.toString()}`;
        } else {
            console.error('No Solana provider found. Install Phantom.');
        }
    } catch (error) {
        console.error('User denied account access', error);
    }
});
