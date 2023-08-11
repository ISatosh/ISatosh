-import hashlib
from datetime import datetime
import json
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.asymmetric import rsa, padding

class Transaction:
    # ...

class Block:
    # ...

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.pending_transactions = []
        self.mining_reward = 50
        self.difficulty = 3

    # ...

    def add_transaction(self, transaction):
        if transaction.verify_signature(transaction.sender) and self.get_balance(transaction.sender) >= transaction.amount:
            self.pending_transactions.append(transaction)

    def mine_block(self, miner_address):
        # ...

    def is_chain_valid(self):
        # ...

    def get_balance(self, address):
        balance = 0
        for block in self.chain:
            for transaction in block.transactions:
                if transaction.sender == address:
                    balance -= transaction.amount
                if transaction.recipient == address:
                    balance += transaction.amount
        return balance

if __name__ == "__main__":
    blockchain = Blockchain()
    miner_address = "Miner1_Address"
    wallet1_private_key = rsa.generate_private_key(
        public_exponent=65537,
        key_size=2048,
        backend=default_backend()
    )
    wallet1_public_key = wallet1_private_key.public_key()

    transaction1 = Transaction(wallet1_public_key, "Recipient_Address", 10)
    data = json.dumps(transaction1.__dict__, sort_keys=True).encode()
    signature = wallet1_private_key.sign(
        data,
        padding.PSS(mgf=padding.MGF1(hashes.SHA256()), salt_length=padding.PSS.MAX_LENGTH),
        hashes.SHA256()
    )
    transaction1.signature = signature

    blockchain.add_transaction(transaction1)
    blockchain.mine_block(miner_address)

    print(f"Saldo do Miner: {blockchain.get_balance(miner_address)}")
    print(f"Saldo do Wallet 1: {blockchain.get_balance(wallet1_public_key)}")

    print(f"A blockchain é válida? {blockchain.is_chain_valid()}")

    # Adicionar mais transações e minerar outros blocos...
# ... Código anterior ...

# Adicionar tratamento de erros
class Blockchain:
    # ...

    def add_transaction(self, transaction):
        try:
            if transaction.is_valid() and self.validate_transaction(transaction):
                self.pending_transactions.append(transaction)
            else:
                raise ValueError("Transaction is not valid or not allowed.")
        except Exception as e:
            print(f"Error adding transaction: {e}")

    # ...

    def mine_block(self, miner_address):
        try:
            # Mineração do bloco
        except Exception as e:
            print(f"Error mining block: {e}")

  

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.pending_transactions = []
        self.difficulty = 3  # Nível de dificuldade da prova de trabalho
        self.mining_reward = 50

    # ...

    def mine_block(self, miner_address):
        try:
            if not self.pending_transactions:
                raise ValueError("No transactions to mine.")
            
            last_block = self.chain[-1]
            new_block = Block(last_block.index + 1, time.time(), self.pending_transactions, last_block.hash)

            proof = self.proof_of_work(new_block)
            new_block.hash = new_block.calculate_hash()
            self.chain.append(new_block)

            # Recompensa para o minerador
            reward_transaction = Transaction("System", miner_address, self.mining_reward)
            self.pending_transactions = [reward_transaction]

            print("Block mined:", new_block)
        except Exception as e:
            print(f"Error mining block: {e}")

    # ...

# ...

if __name__ == "__main__":
    blockchain = Blockchain()
    miner_address = "Miner1_Address"
    wallet1_private_key = "Private_Key1"
    wallet1_public_key = "Public_Key1"

    # ...

    # Adicionar uma transação pendente
    new_transaction = Transaction(wallet1_public_key, "Recipient_Address", 20)
    new_transaction.sign_transaction(wallet1_private_key)
    blockchain.add_transaction(new_transaction)

    # Minerar um bloco
    blockchain.mine_block(miner_address)

    # ...
import hashlib
import time

class Transaction:
    # ... Código da classe Transaction ...

class Block:
    # ... Código da classe Block ...

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.pending_transactions = []
        self.difficulty = 3  # Nível de dificuldade da prova de trabalho
        self.mining_reward = 50

    # ... Métodos anteriores ...

    def validate_transaction(self, transaction):
        # Implemente validações robustas aqui
        return True

    def proof_of_work(self, block):
        # Implemente a prova de trabalho com o nível de dificuldade

    # ...

# ... Outras classes e funcionalidades ...

# Exemplo de uso:
if __name__ == "__main__":
    blockchain = Blockchain()
    miner_address = "Miner1_Address"
    wallet1_private_key = "Private_Key1"
    wallet1_public_key = "Public_Key1"

    # Adicionar uma transação pendente
    new_transaction = Transaction(wallet1_public_key, "Recipient_Address", 20)
    new_transaction.sign_transaction(wallet1_private_key)
    blockchain.add_transaction(new_transaction)

    # Minerar um bloco
    blockchain.mine_block(miner_address)

    # Registrar nós na rede
    node1 = "http://localhost:5001"
    node2 = "http://localhost:5002"
    blockchain.register_node(node1)
    blockchain.register_node(node2)

    # Resolver consenso entre os nós
    consensus_result = blockchain.consensus()
    if consensus_result:
        print("Consensus reached. Blockchain updated.")

    # ... Continuar interagindo com mais funcionalidades ...

# Exemplo de uso (continuação):
if __name__ == "__main__":
    # ... Código anterior ...

    # Criar um contrato inteligente com eventos
    smart_contract = SmartContractWithEvents(contract_owner)
    event_name = "Transfer"
    event_data = {"sender": wallet1_public_key, "recipient": "Recipient_Address", "amount": 20}
    smart_contract.emit_event(event_name, event_data)

    # Visualizar os eventos emitidos pelo contrato
    for event in smart_contract.events:
        print(f"Event: {event['event_name']}, Data: {event['data']}")

    # ... Continuar interagindo com mais funcionalidades ...
# ... Código anterior ...

class SmartContract:
    def __init__(self, contract_owner):
        self.contract_owner = contract_owner

    def execute_operation(self, operation, *args):
        if hasattr(self, operation):
            operation_function = getattr(self, operation)
            return operation_function(*args)
        else:
            return "Operation not supported"

class AdditionContract(SmartContract):
    def __init__(self, contract_owner):
        super().__init__(contract_owner)

    def add_numbers(self, a, b):
        return a + b

# ... Código anterior ...

# Exemplo de uso (continuação):
if __name__ == "__main__":

    # Criar um contrato de adição
    addition_contract = AdditionContract(contract_owner)

    # Executar a operação de adição
    result = addition_contract.execute_operation("add_numbers", 10, 5)
    print("Result of addition:", result)

    # ... Continuar interagindo com mais funcionalidades ...
# ... Código anterior ...

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.pending_transactions = []
        self.difficulty = 3
        self.mining_reward = 50
        self.nodes = set()

    # ... Métodos anteriores ...

    def mine_block(self, miner_address):
        # ... Mineração de um bloco ...

        # Emitir a recompensa para o minerador
        reward_transaction = Transaction("System", miner_address, self.mining_reward)
        self.pending_transactions = [reward_transaction]

# ... Outras classes e funcionalidades ...

# Exemplo de uso (continuação):
if __name__ == "__main__":

    # Adicionar uma transação pendente
    new_transaction = Transaction(wallet1_public_key, "Recipient_Address", 20)
    new_transaction.sign_transaction(wallet1_private_key)
    blockchain.add_transaction(new_transaction)

    # Minerar um bloco
    blockchain.mine_block(miner_address)

    # ... Continuar interagindo com mais funcionalidades ...
# ... Código anterior ...

class SmartContract:
    def __init__(self):
        self.contracts = {}

    def deploy_contract(self, contract_name, contract):
        self.contracts[contract_name] = contract

    def execute_contract(self, contract_name, operation, *args):
        if contract_name in self.contracts:
            contract = self.contracts[contract_name]
            if hasattr(contract, operation):
                operation_function = getattr(contract, operation)
                return operation_function(*args)
            else:
                return "Operation not supported"
        else:
            return "Contract not found"

class TokenContract:
    def __init__(self):
        self.balances = {}

    def create_tokens(self, address, amount):
        if address not in self.balances:
            self.balances[address] = amount
        else:
            self.balances[address] += amount

    def transfer_tokens(self, sender, recipient, amount):
        if sender in self.balances and self.balances[sender] >= amount:
            self.balances[sender] -= amount
            if recipient not in self.balances:
                self.balances[recipient] = amount
            else:
                self.balances[recipient] += amount
            return True
        return False

# Exemplo de uso (continuação):
if __name__ == "__main__":
    # ... Código anterior

    # Criar um contrato de tokens
    token_contract = TokenContract()
    contract_name = "TokenContract"
    smart_contract.deploy_contract(contract_name, token_contract)

    # Executar operações no contrato de tokens
    smart_contract.execute_contract(contract_name, "create_tokens", wallet1_public_key, 100)
    smart_contract.execute_contract(contract_name, "create_tokens", "Recipient_Address", 50)
    smart_contract.execute_contract(contract_name, "transfer_tokens", wallet1_public_key, "Recipient_Address", 30)

    # Verificar saldos após as operações
    print(f"Balance of {wallet1_public_key}: {token_contract.balances.get(wallet1_public_key, 0)} tokens")
    print(f"Balance of Recipient_Address: {token_contract.balances.get('Recipient_Address', 0)} tokens")

    # ... Continuar interagindo com mais funcionalidades ...
# ... Código anterior ...

class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
        self.difficulty = 4
        self.pending_transactions = []
        self.mining_reward = 100
        self.nodes = set()

    # ... Métodos anteriores ...

    def mine_pending_transactions_auto(self, miner_address):
        # Mineração de blocos automaticamente quando há transações pendentes suficientes
        while len(self.pending_transactions) > 0:
            new_block = Block(len(self.chain), self.chain[-1].hash, self.pending_transactions)
            new_block.mine_block(self.difficulty)
            self.chain.append(new_block)
            print("Block mined:", new_block.hash)
            self.pending_transactions = [Transaction("System", miner_address, self.mining_reward)]

    def get_balance(self, address):
        balance = 0
        for block in self.chain:
            for tx in block.transactions:
                if tx.sender == address:
                    balance -= tx.amount
                if tx.recipient == address:
                    balance += tx.amount
        return balance

# Exemplo de uso (continuação):
if __name__ == "__main__":

    # Atualização automática da blockchain (mineração contínua)
    print("Mining blocks automatically...")
    blockchain.mine_pending_transactions_auto(miner_address)

    # Verificar saldos após mineração automática
    print(f"Balance of {wallet1_public_key}: {blockchain.get_balance(wallet1_public_key)} tokens")
    print(f"Balance of Recipient_Address: {blockchain.get_balance('Recipient_Address')} tokens")

    # ... Continuar interagindo com mais funcionalidades ...

 👋 Hi, I’m @ISatosh
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
ISatosh/ISatosh is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
