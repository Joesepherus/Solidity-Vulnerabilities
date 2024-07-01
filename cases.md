<h2>Cases of Solidity Vulnerabilities Exploited</h2>


<div>
    <h3>Uranium Finance</h3>
    Changing values in standardised contract, but forgetting to change them in one instance. Missplaced zero.
</div>

<div>
    <h3>Poly Network</h3>
    Calling a function from a contract to another contract that can change the "keepers" or owners that verify transactions. And then just sent the funds to your wallet address.
</div>

<div>
    <h3>Cream Finance Hack</h3>
    Reentrancy Attack
</div>



<div>
<h3>Multi signature Wallet(The Parity Wallet Bug)</h3>
In 2017 they had a library that was not initialized, but anyone could set the owner and then destroy it. Thus anyone using this library lost their money. All multi signature wallets people had used this library and they all together lost $280m.
</div>

<div>
<h3>Crypto Punks</h3>
They had the initialize function public, so anyone could change the forge address to their address and then use the withdraw function to send them all the funds from the contract.
</div>

<div>
<h3>SafeMoon Exploit</h3>
What happened with Safemoon is that they allowed anyone to burn tokens. So what the attacker did was he bought a lot of safe moon tokens and then called the function to burn a lot of the tokens and that made the price go up and then he proceeded to sell his safe moon tokens and made millions from this. He basically artificially made the token price go up temporarily and sold off on the high. Genius really.
<a href="https://www.immunebytes.com/blog/safemoon-exploit-mar-28-2023-detailed-analysis/" target="_blank" rel="noopener noreferrer">link</a>
</div>

<div>
<h3>Seneca Protocol Attack</h3>
<p>So Seneca Protocol was hacked by calling performActions and inside there calling a function _call which was set to a constact "30". Then from there on you can call anything using the callData. So the attack called the standard ERC20 function transferFrom and as data he set the from address a victim address and to address his address and any arbitrary value of ether. 
</p>
<p>And that's how the attacker was able to steal money from Seneca. What a dumb way to go really. And you would think these kinds of attacks wouldn't happen anymore, so trivial to secure your damn call functions giving anyone the power to call anything is beyond me haha. This hack happened very recently in February 2024.
</p>
<a href="https://github.com/SenecaDefi/SenecaProtocol/blob/main/contracts/Chamber.sol" target="_blank" rel="noopener noreferrer">Seneca Protocol Chamber</a>
<a href="https://www.cyfrin.io/blog/seneca-attack-hack-analysis-proof-of-concept" target="_blank" rel="noopener noreferrer">link</a>
<a href="https://rekt.news/seneca-protocol-rekt/" target="_blank" rel="noopener noreferrer">link 2</a>
</div>

<div>
    <h4>My thoughts</h4>
    <pre><code>What I also see quite often is that they abuse the call function. By doing that you can call some other contract function(in the name of the contract you're calling it from, so not from your own) even some contract that they imported. Crazy stuff.</pre></code>
</div>