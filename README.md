# solidity--programs
# we mainly create smart contracts
# activity 1 hello world program
pragma solidity 0.8.19;
contract sindhu{
    string a;
    function scan(string memory b)public{
        a=b;
    }
    function print()public view returns(string memory){
        return a;
    }
-------------------------------------------------------------------------------------------------------------------------------------------------
# activity 2 smart contract by using arrays
pragma solidity 0.8.19;
contract sindhu{
string[]a;
    function scan(string memory b)public{
        a.push(b);
    }
    function print()public view returns(string[] memory){
        return a;
    }
-------------------------------------------------------------------------------------------------------------------------------------------------
# activity 3  restrict constructor
pragma solidity 0.8.19;
contract sindhu{
    address owner;
    string a;
    constructor(){//constructor
        owner=msg.sender;
    }
    //admin only
    function func1()public {
       require(owner==msg.sender);
       a="admin only";
    }
    //any one
    function func2()public {
        a="anyone";
    }
    //any one
    function print() public view returns(string memory){
        return a;
    }
--------------------------------------------------------------------------------------------------------------------------------------------------------
# activity 4 using constructor
pragma solidity 0.8.19;
contract sindhu{
    address public owner;
    constructor(){
       owner=msg.sender;
    }
  }
-----------------------------------------------------------------------------------------------------------------------------------------------------------  
  
