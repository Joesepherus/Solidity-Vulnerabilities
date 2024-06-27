<h3>Include SPDX-License-Identifier</h3><p></p><h3>You should fix the Solidity version to the compiler you are using.</h3><p>Dont use this</p><pre><code>pragma solidity ^0.8.0;</code></pre><p>Use this</p><pre><code>pragma solidity 0.8.21;</code></pre><p><br>Explicitly set the library version in the import statement</p><p></p><h3>Use named imports instead of importing the entire namespace</h3><p>Instead of doing this</p><pre><code>import "@openzeppelin/contracts@4.9.3/token/ERC20/ERC20.sol";</code></pre><p>Do this</p><pre><code>import {ERC20} from "@openzeppelin/contracts@4.9.3/token/ERC20/ERC20.sol";</code></pre><p></p><h3>Delete unused imports</h3><p></p><h3>Apply contract-level natspec</h3><p>An example natspec for a contract is shown below.</p><pre><code>/// @title Liquidity token for Foo protocol
/// @author Foo Incorporated
/// @notice Notes for non-technical readers/
/// @dev Notes for people who understand Solidity
contract LiquidityToken {

}</code></pre><p></p><h3>Lay out the contract structure per the style guide</h3><p>They should be ordered as follows: type declarations, state variables, events, errors, modifiers, receive and fallback functions (if applicable), external functions, public functions, internal functions, and private functions.</p><p>Within those groups, the payable functions go on top, then non-payable, then view, then pure.</p><p></p><h3>Replace magic numbers with constants</h3><p>Generally, numbers should be written as a constant at the top of the contract.</p><h3><br>If numbers are used to measure ether or time, use the solidity keywords</h3><p>Instead of writing</p><pre><code>uint256 secondsPerDay = 60 * 60 * 24;</code></pre><p>do</p><pre><code>1 days;</code></pre><p>instead of writing</p><pre><code>require(msg.value == 10**18 / 10, "must send 0.1 ether");</code></pre><p>do</p><pre><code>require(msg.value == 0.1 ether, "must send 0.1 ether");</code></pre><p></p><h3>Use underscores to make large numbers more readable</h3><p>Instead of doing this</p><pre><code>uint256 private constant BASIS_POINTS_DENOMINATOR = 10000</code></pre><p>do this</p><pre><code>uint256 private constant BASIS_POINTS_DENOMINATOR = 10_000</code></pre><p></p><h3>Remove the virtual modifier from functions that will not be overridden</h3><p>The virtual modifier means “overridable by a child contract.” But if you know you will not be overriding the function (because you are the deployer), then this modifier is superfluous. Just delete it.</p><h3><br>Put function modifiers in the correct order visibility, mutability, virtual, override custom modifier</h3><p></p><pre><code>// visibility (payability), [virtual], [override], [custom]
function foo() public payable onlyAdmin {

}

function bar() internal view virtual override onlyAdmin {

}</code></pre><p></p><h3>Use natspec properly for functions</h3><p>The rules are similar to the contract natspec, except that we also specify params based on the function arguments and what gets returned.</p><pre><code>/// @notice Deposit ERC20 tokens
/// @dev emits a Deposit event
/// @dev reverts if the token is not allowlisted
/// @dev reverts if the contract is not approved by the ERC20
/// @param token The address of the ERC20 token to be deposited
/// @param amount The amount of ERC20 tokens to deposit
/// @returns the amount of liquidity tokens the user receives
function deposit(address token, uint256 amount) public returns (uint256) {

}

// If the contract inherits functions, you can also inherit their natspec
/// @inheritdoc Lendable
function calculateAccumulatedInterest(address token, uint256 since) public override view returns (uint256 interest) {

} </code></pre><p></p><p>For the dev parameters, it’s good to notify what kind of state changes it can do, for example emitting an event, sending ether, selfdestructing, etc.</p><p>The notice and param natspec are read by Etherscan.</p><p></p><h3>Remove commented out code</h3><p></p><h3>Think carefully about variable names</h3><p></p><h2>Additional Tricks for organizing large codebases</h2><ul><li><p>If you have a lot of storage variables, you can define all the storage variables in a single contract, then inherit from that contract to gain access to those storage variables.</p></li><li><p>If your functions require a significant amount of parameters, use a struct to pass the information around.</p></li><li><p>If you need a lot of imports, you can import all the files and types into one solidity file, then import that file (you would need to intentionally break the rule about named imports).</p></li><li><p>Use libraries to group functions of the same category together and make files smaller.</p></li></ul>