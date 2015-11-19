The BitGo Platform API
Build your Bitcoin application on the secure and scalable foundation chosen by the world’s leading exchanges and institutions. Learn more at bitgo.com/platform.
Robust Wallet API and SDKs
Our API and SDKs take the difficulty out of Bitcoin and multi-sig. They expose simple, single-call interfaces to provision wallets, create addresses, view balances/transactions, send coins, and perform many other Bitcoin operations. Integration is seamless and can be as simple as a 1-line code change if you already use bitcoind.

Trustless Multi-Sig Model
BitGo uses a 2-of-3 trustless multi-sig model where you hold custody of 2 keys, putting you in full control of your funds. BitGo SDKs handle all private key information and signing client-side, so your key is never sent in the open. 

Powerful, Policy-Backed Co-Signer
During day-to-day operations, BitGo co-signs every outgoing transaction from your wallet, ensuring that wallet spends meet a comprehensive set of policies before going out to the network. Policy engine rules include transfer velocity limits, bitcoin address whitelisting, time-of-day restrictions, 2FA requirements, IP address lockdown, and oracle callbacks. 

Reliable Blockchain Data
Our API and SDKs give you full, unified access to the blockchain, taking out the cost and complexity of running your own infrastructure. 

Insurance-Backed Guarantee
BitGo has comprehensive bitcoin theft insurance from XL Group, a global, A-rated underwriter. All BitGo customers are automatically protected from theft and loss for up to $250,000 and can opt-in to an additional insurance-backed guarantee from BitGo.


BitGo SDK Quick Start Guide
Detailed docs at https://test.bitgo.com/api. Help on site and at hackathonhelp@bitgo.com. 

Sign Up
Go to https://test.bitgo.com/ and sign up for an account. 
This account will operate on the Bitcoin Testnet and is seperate from accounts created at https://www.bitgo.com/ (production).
In the account, obtain a developer access token from Settings->Developers and save it.

Install and initialize SDK
Ensure you have nodeJS/npm installed.
Do npm install -g bitgo or clone our opensource GitHub: https://github.com/BitGo/BitGoJS
Start a javascript intepreter (node) and load the module:
	var BitGo = require('bitgo');
var bitgo = new BitGo.BitGo({ accessToken: ‘ACCESSTOKENFROMABOVE’ });
 
Create a Wallet
var wallet;
var params = { "passphrase": "replaceme", "label": "firstwallet",  "backupXpub": "xpub6AHA9hZDN11k2ijHMeS5QqHx2KP9aMBRhTDqANMtdyw2TDYRmF8P.." }
bitgo.wallets().createWalletWithKeychains(params, function(err, result) {
  wallet = result.wallet; 
  console.dir(wallet.wallet);
  console.log("New user keychain encrypted xPrv: " + result.userKeychain.encryptedXprv); // created locally
});

Create a New Bitcoin Address
wallet.createAddress({ "chain": 0 }, function callback(err, address) {
    console.dir(address);
});

Now you can deposit test coins into the address. Get some here: http://tpfaucet.appspot.com/

View Transactions
wallet.transactions({}, function callback(err, transactions) {
    console.dir(transactions);
});

Send Coins
wallet.sendCoins({ address: "2NEe9QhKPB2gnQLB3hffMuDcoFKZFjHYJYx", amount: 0.01 * 1e8, walletPassphrase:  "replaceme" }, function(err, result) {
    console.dir(result);
});
When you get the txhash back, you can view the transaction at http://tbtc.blockr.io/tx/info/<HASH>
How to set a policy rule:

> var rule = {
...             id: "webhookRule1",
...             type: "webhook",
...             action: { type: "deny" },
...             condition: { "url": 'https://17fc38db.ngrok.com/poll' }
...           };
undefined
>
> wallet.setPolicyRule(rule, function callback(err, w) { console.dir(w); });


code for the remote endpoint:
app.post('/poll', function(req, res, next) {
 var webhookData = req.body;
 var theOutput;
 webhookData.outputs.forEach(function(output) {
   if (output.outputWallet !== webhookData.walletId) { theOutput = output.outputAddress; }
 });

 var url = "https://www.polleverywhere.com/discourses/llb3d9yZe89MQA7.json?humanize=false&_=" + Math.random()*10000000;

 var request = require('request');
 x = request.get(url, function (error, response, body) {
   if (!error && response.statusCode == 200) {
     var pollData = JSON.parse(response.body);
     console.dir(pollData.results);
     var winningAddress = '';
     var winningUpvotes = 0;
     pollData.results.forEach(function(result) {
       if (result.upvotes > winningUpvotes) {
         winningAddress = result.value;
       }
     });
     console.log('winning address: ' + winningAddress);
     if (theOutput === winningAddress) {
       res.status(200).send({});
     } else {
       res.status(400).send({});
     }
   } else {
     console.log('error');
     console.dir(error);
   }
 });
});
