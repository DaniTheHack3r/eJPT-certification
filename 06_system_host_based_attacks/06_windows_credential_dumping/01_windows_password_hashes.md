# Windows Password Hashes

- The Windows OS stores hashed user account passwords locally in the SAM (Security Accounts Manager) database.

- Hashing is the process of converting a piece of data into another value. A hashing function or algorithm is used to generate the new value. The result of a hashing algorithm is known as a hash or hash value.

- Authentication and verification of user credentials is facilitated by the Local Security Authority (LSA).

- Windows versions up to Windows Server 2003 utilize two different types of hashes:
    + LM
    + NTLM

- Windows disables LM hashing and utilizes NTLM hashing from Windows Vista onwards.

**Note**: LM hash is difficult to come by in the wild as it is only available in very old windows systems.

## SAM Database

- SAM (Security Account Manager) is a database file that is responsible for managing user accounts and passwords on Windows. All user account passwords stored in the SAM database are hashed.

- The SAM database file cannot be copied while the operating system is running.

- The Windows NT kernel keeps the SAM database file locked and as a result, attackers typically utilize in-memory techniques and tools to dump SAM hashes from the LSASS (Local Security Authority Sub System) process.

**Note**: LSASS is in charge of authentication in windows and it will typically carry NTLM hashes in cache as it interacts with the SAM database.

- In modern versions of Windows, the SAM database is encrypted with a syskey.

**Note**: Elevated/Administrative privileges are required in order to access and interact with the LSASS process.

## LM (LanMan)

- LM is the default hashing algorithm that was implemented in Windows operating systems prior to NT4.0.

- The protocol is used to hash user passwords, and the hashing process can be broken down into the following steps:
    + The password is broken into two seven-character chunks.
    + All characters are then converted into uppercase.
    + Each chunk is then hashed separately with the DES algorithm.

- LM hashing is generally considered to be a weak protocol and can easily be cracked, primarily because the password hash does not include salts, consequently making brute-force and rainbow table attacks effective against LM hashes.

**Note**: Refer to the course file to page 75 of the pdf to see a graphical representation.

## NTLM (NTHash)

- NTLM is a collection of authentication protocols that are utilized in Windows to facilitate authentication between computers. The authentication process involves using a valid username and password to authenticate successfully.

- From Windows Vista onwards, Windows disables LM hashing and utilizes NTLM hashing.

- When a user account is created, it is encrypted using the MD4 hashing algorithm, while the original password is disposed of.

- NTLM improves upon LM in the following ways:
    + Does not split the hash in to two chunks.
    + Case sensitive.
    + Allows the use of symbols and unicode characters.

**Note**: NTLM are relatively easy to crack, through a brute force attack or a rainbow table attack, as they do not have password salts.

**Note**: Refer to the system host based attacks course file to page 77 of the pdf to see a graphical representation.
