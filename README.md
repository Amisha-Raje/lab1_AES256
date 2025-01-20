# lab1_AES256

# AES-256 Encryption/Decryption Tool

A Python implementation of AES-256 encryption and decryption with built-in performance analysis capabilities. This tool offers secure file encryption using AES-256 in CBC mode, along with features for performance testing and data visualization.
## Features

-Secure AES-256 encryption and decryption in CBC mode
-File encryption and decryption functionality
-Performance analysis with visual representations
-Generation of cryptographically secure random keys
-Robust error handling and input validation

## Security Considerations

- Utilizes CBC mode with reliable padding mechanisms  
- Incorporates initialization vector (IV) for improved security  
- Leverages secure random number generation techniques  
- Features comprehensive error handling for cryptographic processes  

## Prerequisites

- Python 3.7 or higher
- pip (Python package installer)

## Installation

1. Clone this repository:

```bash
git clone https://github.com/yourusername/aes-encryption-tool.git
cd aes-encryption-tool
```

2. Create and activate a virtual environment (recommended):

```bash
python -m venv venv
source venv/bin/activate  # On Windows, use: venv\Scripts\activate
```

3. Install required dependencies:

```bash
pip install pycryptodome matplotlib
```

## Usage

### Basic Usage

1. Create a file named `plaintext.txt` with your content.

2. Run the script:

```bash
python encryption_tool.py
```

This will:

- Generate a new encryption key
- Encrypt `plaintext.txt` to `encrypted.bin`
- Decrypt `encrypted.bin` to `decrypted.txt`
- Run performance tests and display results

### API Usage

```python
from encryption_tool import generate_key, encrypt_file, decrypt_file

# Generate a new key
key = generate_key()

# Encrypt a file
encrypt_file(key, "input.txt", "encrypted.bin")

# Decrypt a file
decrypt_file(key, "encrypted.bin", "decrypted.txt")
```

## Code Explanation

### Key Components

1. **Key Generation**  
   - Leverages `get_random_bytes` from PyCryptodome to ensure secure key generation.  
   - Produces 256-bit (32-byte) keys, compliant with AES-256 specifications.  

2. **Encryption Process**  
   ```python  
   def encrypt_data(key, plaintext):  
       cipher = AES.new(key, AES.MODE_CBC)  
       ciphertext = cipher.encrypt(pad(plaintext.encode('utf-8'), BLOCK_SIZE))  
       return cipher.iv + ciphertext  
   ```  
   - Initializes an AES cipher in CBC mode for encryption.  
   - Pads plaintext data to meet block size requirements.  
   - Prepends the IV to the ciphertext to facilitate decryption.  

3. **Decryption Process**  
   ```python  
   def decrypt_data(key, ciphertext):  
       iv = ciphertext[:BLOCK_SIZE]  
       actual_ciphertext = ciphertext[BLOCK_SIZE:]  
       cipher = AES.new(key, AES.MODE_CBC, iv)  
       return unpad(cipher.decrypt(actual_ciphertext), BLOCK_SIZE)  
   ```  
   - Extracts the IV from the ciphertext header.  
   - Uses the extracted IV to recreate the AES cipher for decryption.  
   - Strips padding to recover the original plaintext.  

4. **Performance Testing**  
   - Evaluates encryption and decryption performance for various input sizes.  
   - Generates visualizations of performance metrics using `matplotlib`.  
   - Logs encryption and decryption timing for precise analysis.  

---

## **Security Best Practices**  

1. **Key Management**  
   - Avoids storing keys directly in source code.  
   - Encourages the use of secure key storage solutions (e.g., environment variables, hardware security modules).  
   - Implements key rotation strategies for enhanced security.  

2. **Error Handling**  
   - Wraps all cryptographic operations in `try-except` blocks for error resilience.  
   - Provides meaningful error messages to aid in debugging.  
   - Protects against information leakage by ensuring secure error reporting.  

3. **Input Validation**  
   - Confirms the existence and accessibility of input files.  
   - Ensures proper encoding of input data to maintain compatibility.  
   - Handles padding appropriately to prevent decryption errors.  

---

## **Performance Considerations**  
- Tests encryption and decryption for input sizes ranging from 1KB to 16KB.  
- Measures execution times and evaluates performance trends.  
- Visualizes results with `matplotlib` for clear insights.  

---

## **Limitations**  
- Limited to CBC mode for encryption operations.  
- Processes files synchronously, which might affect scalability.  
- May encounter performance challenges with very large in-memory files.  
