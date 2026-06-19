# PQC (Post-Quantum Cryptography)

**Since Camel 4.16**

The PQC data format supports encrypting and decrypting payload using Post Quantum Cryptography algorithms.

## PGC DataFormat Options

The PQC (Post-Quantum Cryptography) dataformat supports 7 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **keyEncapsulationAlgorithm** (common) | `MLKEM` | `Enum` | 
The Post-Quantum KEM algorithm to use for key encapsulation. Supported values: MLKEM, BIKE, HQC, CMCE, SABER, FRODO, NTRU, NTRULPRime, SNTRUPrime, KYBER.

Enum values:

-   MLKEM
    
-   BIKE
    
-   HQC
    
-   CMCE
    
-   SABER
    
-   FRODO
    
-   NTRU
    
-   NTRULPRime
    
-   SNTRUPrime
    
-   KYBER
    





 |
| **symmetricKeyAlgorithm** (common) | `AES` | `Enum` | 

The symmetric encryption algorithm to use with the shared secret. Supported values: AES, ARIA, RC2, RC5, CAMELLIA, CAST5, CAST6, CHACHA7539, etc.

Enum values:

-   AES
    
-   ARIA
    
-   RC2
    
-   RC5
    
-   CAMELLIA
    
-   CAST5
    
-   CAST6
    
-   CHACHA7539
    
-   DSTU7624
    
-   GOST28147
    
-   GOST3412\_2015
    
-   GRAIN128
    
-   HC128
    
-   HC256
    
-   SALSA20
    
-   SEED
    
-   SM4
    
-   DESEDE
    





 |
| **symmetricKeyLength** (common) | `128` | `Integer` | The length (in bits) of the symmetric key. |
| **keyPair** (common) |  | `Object` | Refers to the KeyPair to lookup from the register to use for KEM operations. |
| **bufferSize** (advanced) | `4096` | `Integer` | The size of the buffer used for streaming encryption/decryption. |
| **provider** (advanced) |  | `String` | The JCE security provider to use. |
| **keyGenerator** (advanced) |  | `Object` | Refers to a custom KeyGenerator to lookup from the register for KEM operations. |