import hashlib
import time

class SnowBlock:
    def init(self, index, previous_hash, timestamp, data):
        self.index = index
        self.previous_hash = previous_hash
        self.timestamp = timestamp
        self.data = data
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        block_string = f"{self.index}{self.previous_hash}{self.timestamp}{self.data}"
        return hashlib.sha256(block_string.encode()).hexdigest()

def create_genesis_block():
    return SnowBlock(0, "0", time.time(), "Genesis Block - Snow")

def create_new_block(previous_block, data):
    index = previous_block.index + 1
    timestamp = time.time()
    previous_hash = previous_block.hash
    return SnowBlock(index, previous_hash, timestamp, data)

# Create Snow blockchain
snow_blockchain = [create_genesis_block()]

# Add more blocks
block_1 = create_new_block(snow_blockchain[-1], "Snow Transaction 1")
snow_blockchain.append(block_1)

block_2 = create_new_block(snow_blockchain[-1], "Snow Transaction 2")
snow_blockchain.append(block_2)

# Print the Snow blockchain
for block in snow_blockchain:
    print(f"Block #{block.index}")
    print(f"Timestamp: {block.timestamp}")
    print(f"Data: {block.data}")
    print(f"Hash: {block.hash}")
    print(f"Previous Hash: {block.previous_hash}")
    print("-" * 40)
