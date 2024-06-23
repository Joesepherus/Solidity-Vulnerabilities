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
    <h4>My thoughts</h4>
    <pre><code>What I also see quite often is that they abuse the call function. By doing that you can call some other contract function(in the name of the contract you're calling it from, so not from your own) even some contract that they imported. Crazy stuff.</pre></code>
</div>