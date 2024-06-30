<h2>Tornado Cash Exploit - Deploy Two Different Contracts at The Same Address</h2>
<p>This happened to Tornado Cash Hack, where the attacker was able to create a contract get approved function by the tornado cash contract, then create another contract at the same address and run his malicious code that was not really approved.</p>
<p>How this works is you create a deployer contract with the function create2 this way you can create a contract with deterministic address.</p>
<p>Then from that deployer contract that you just create you use function create to create the supposedly innocent looking contract that gets approved to be run by tornado cash contract.</p>
<p>Then you selfdestruct the innocent contract and self destruct the deployer contract.</p>
<p>You create the deployer contract again at the deterministic address because you need to reset the nonce and have the same sender address.</p>
<p>And then you finally deploy your malicious contract at the same address as the innocent contract was deployed from your deployer contract.</p>
<p>Becuase the way create works is it takes the sha hash of sender address + its nonce to create the new contract.</p>
<p>And when you delete the deployer contract and deploy it again you have the same sender address and you have reset the nonce counter, so this allows you to create the malicious contract at the same address where the innocent contract was</p>
<p>And by using delegatecall you can change the state of the actual tornado cash contract and take control over it</p>