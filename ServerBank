import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract serverBank is Ownable{
	event Withdraw(string username, address to, uint256 amount);
    event Deposit(string username, address depositer, uint256 amount);
    
    mapping(address => uint256) public allowed;
    
    ERC20 _token;
    
    constructor(address token){
        _token = ERC20(token);
    }
	
	function deposit(string memory username, uint256 amountToDeposit) payable public {
        _token.transferFrom(msg.sender, address(this), amountToDeposit);
        allowed[msg.sender] += amountToDeposit;
        emit Deposit(username, msg.sender, amountToDeposit);
    }

    function getAllowed (address addr) public view returns(uint256){
        return allowed[addr];
    }
    
    function increaseAllowed(address addr, uint256 amount) public onlyOwner returns(uint256){
        allowed[addr] += amount;
        return allowed[addr];
    }
    
    function withdraw(string memory username, uint256 amountToWithdraw) payable public {
        
        
        require(allowed[msg.sender] >= amountToWithdraw);
        
        _token.approve(address(this), amountToWithdraw);

        _token.transferFrom(address(this), msg.sender, amountToWithdraw);

        allowed[msg.sender] -= amountToWithdraw; 

        emit Withdraw(username, msg.sender, amountToWithdraw);

    }
}