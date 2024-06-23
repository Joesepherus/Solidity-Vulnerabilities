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