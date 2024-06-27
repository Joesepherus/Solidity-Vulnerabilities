<h2>What is Contract with Zero Code Size Exploit></h2>
<div>
<p>
Developers use to distinguish between EOA and contract by the code size. If it's EOA the code size is 0, if a contract then its > 0.
</p>
<p>
This is a bad practice because the extcodesize opcode returns the code size of the runtime code, so if we call the extcodesize while the constructor is still running, the code size will be 0, because the runtime code is not deployed yet.
</p>
<h3>Solution</h3>
<p>The solution in this kind of situation is to avoid using this pattern at all. It was even removed from the OpenZeppelin Address library in a recent new version, for this very reason.<p>
</div>