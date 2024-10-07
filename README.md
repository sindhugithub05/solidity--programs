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
 # activity 6 
 pragma solidity 0.8.19;
 contract sindhu{
    address owner;
    string a;
    constructor(){
        owner=msg.sender;
    }
    function func1()public {
       require(owner==msg.sender);
       a="admin only";
    }
    function func2()public {
        a="anyone";
    }
    function print() public view returns(string memory){
        return a;
    } 
}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# activity 7 using mapping  data type
pragma solidity 0.8.19;
contract sindhu
{
 string[]_msg;
    mapping(string=>bool)_unique;
    function scan(string memory b)public{
        require(!_unique[b]);
        _msg.push(b);
        _unique[b]=true;
    }
    function print() public view returns(string[] memory){
        return _msg;
    }
 }
 ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# activity 8 fake product detection
pragma solidity 0.8.19;
contract sindhu
{
    struct products{
        uint id;
        string name;
        bool exists;
    }
    mapping(uint=>products)_list;
    function addproduct(uint i,string memory n)public{
        require(!_list[i].exists);
        products memory new_product=products(i,n,true);
        _list[new_product.id]=new_product;
    }
    function verifyproduct(uint i) public view returns(string memory){
        if(_list[i].id==i)
          return "Original";
        else 
          return "fake";  
    }
}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 # activity 9 voting system
 pragma solidity 0.8.19;
 contract sindhu
 {
    uint[3]_votes;
    mapping(address=>bool)_voters;
    constructor(){
        _votes[0]=0;
        _votes[1]=0;
        _votes[2]=0;
    }
    function castvote(uint id)public{
        require(!_voters[msg.sender]);
        if(id==0)
         _votes[0]++;
        else if(id==1)
         _votes[1]++;
        else if(id==2)
         _votes[2]++;
        _voters[msg.sender]=true;
    }
    function result() public view returns(uint[3] memory) {
        return _votes;
    }
}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# activity 10 login a platform
pragma solidity 0.8.19;
contract sindhu{
    struct users{
        string username;
        string password;
        bool valid;
    }
    mapping(string=>users)_users;
    function compare(string memory a,string memory b) public  pure returns(bool){
        bytes memory bytesA=bytes(a);
        bytes memory bytesB=bytes(b);
        if(bytesA.length!=bytesB.length)
          return false;
        bytes32 hashA=keccak256(bytesA);
        bytes32 hashB=keccak256(bytesB);
        return(hashA==hashB);
    }
    function signup(string memory u,string memory p)public{
        require(!_users[u].valid);
        users memory new_user=users(u,p,true);
        _users[new_user.username]=new_user;
    }
    function login(string memory u,string memory p)public view returns(bool){
        if((compare(_users[u].username,u))&&(compare(_users[u].password,p)))
         return true;
        else 
         return false;
    }
}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# activity 11 supply chain management
pragma solidity 0.8.19;
contract sindhu
{
    address owner;
    struct product{
        uint id;
        string name;
        bool valid;
        string distributor;
        string retailer;
        bool isDistributed;
        bool isRetailed;
    }
    mapping(uint=>product)products;
    constructor(){
        owner=msg.sender;
    }
    function addproduct(uint i,string memory n)public{
        require(owner==msg.sender);
        require(!products[i].valid);
        product memory new_product=product(i,n,true,owner,owner,false,false);
        products[new_product.id]=new_product;
    }
    function addDistributor(uint i,address d)public{
        require(products[i].valid);
        require(!products[i].isDistributed);
        products[i].distributor=d;
        products[i].isDistributed=true;
    }
     function addDistributor(uint i,address r)public{
        require(products[i].valid);
        require(products[i].isDistributed);
        require(!products[i].isRetailed);
        products[i].retailed=r;
        products[i].isRetailed=true;
    }
    function verify(uint i)public view returns(product memory){
        return products[i];
    }
}
 
