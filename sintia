pragma solidity ^0.4.2;

contract Sintia {
    // Informació pública del token
    string public name = "Sintia";
    string public symbol = "SNT";
    string public standard = "SNT v.1.1";
    uint256 public totalSupply;

    // Esdeveniments que informen de les transferències i aprovacions
    event Transfer(
        address indexed _from,
        address indexed _to,
        uint256 _value
    );

    event Approval(
        address indexed _owner,
        address indexed _spender,
        uint256 _value
    );

    // Mappings per a gestionar balanços i permisos
    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    // Constructor del contracte, assigna el subministrament inicial al creador
    function Sintia (uint256 _initialSupply) public {
        balanceOf[msg.sender] = _initialSupply;
        totalSupply = _initialSupply;
    }

    // Funció per transferir tokens entre adreces
    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(balanceOf[msg.sender] >= _value); // Comprova que el remitent té prou saldo
        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;

        // Dispara l'esdeveniment de transferència
        Transfer(msg.sender, _to, _value);

        return true;
    }

    // Funció per aprovar un tercer per gastar tokens en nom teu
    function approve(address _spender, uint256 _value) public returns (bool success) {
        allowance[msg.sender][_spender] = _value; // Assigna el permís d'ús de tokens

        // Dispara l'esdeveniment d'aprovació
        Approval(msg.sender, _spender, _value);

        return true;
    }

    // Funció perquè un tercer faci una transferència en nom d'un altre (com a ERC-20)
    function transferFrom(address _from, address _to, uint256 _value) public returns (bool success) {
        require(_value <= balanceOf[_from]); // Comprova que el remitent té prou saldo
        require(_value <= allowance[_from][msg.sender]); // Comprova que l'enviador té permís per fer la transacció
        
        // Actualitza els saldos i el permís restant
        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;
        allowance[_from][msg.sender] -= _value;

        // Dispara l'esdeveniment de transferència
        Transfer(_from, _to, _value);

        return true;
    }
}
