<h2>What is Re-entrancy attack?</h2>
<div>
<p>
A reentrancy attack occurs when a function makes an external call to another untrusted contract. Then the untrusted contract makes a recursive call back to the original function in an attempt to drain funds.</p>
<p>When the contract fails to update its state before sending funds, the attacker can continuously call the withdraw function to drain the contract’s funds.<p>
</div>

<h2>How to fight against Re-entrancy attack?</h2>
Update balances internally before calling external code/contract
Use function modifiers that prevent reentrancy

<pre><code>contract ReEntrancyGuard {
    bool internal locked;

    modifier noReentrant() {
        require(!locked, "No re-entrancy");
        locked = true;
        _;
        locked = false;
    }
}
</code></pre>