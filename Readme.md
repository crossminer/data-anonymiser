
# Presentation

This Perl module provides utilities to anonymise data, in the context of dataset generation. The idea basically is to encrypt the data with a private/public key system and then throw away the keys. It has the following properties:

* Retrieving the original data is close to impossible, according to current cryptographic systems. One can still, for debugging purposes, get the original data back if the key is saved. For production or final releases the key should not be saved anywhere to ensure privacy.
* It still preserves one-to-one relationship between original data and encrypted data, with as little collisions as possible. This is especially useful for research analysis, where one can detect identical items without knowing the protected data.

It is ok to truncate hashes, and encoding base64 makes the collision risk a bit lower. For a good explanation see [hash function that produces short hashes](https://stackoverflow.com/questions/4567089/hash-function-that-produces-short-hashes) on StackOverflow.

# Requirements

In our use case we want to be able to anonymise the following types of data:

* UUIDs, whatever they are.
* Email addresses
* Java classes (by class? or by full path?)

We want to have a one-to-one relationship from original data to encrypted data, so as to identify identical entries without knowing them.

We want a method that prevent any reconstruction of the original data, according to the current state of research on privacy.

# Test output

```
* Test create_keys
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA0sHCiS8B1x0qLaeuJfLPE49K2fw5x4cp
CoYpjYFECjuxNSEMUA5RlEBD37nesMK6ftEA3dVmtDtroA3EHG5NrbVqXCFKBAksdaLpDGPaemsA
rMKo+D1rNQem6jF/aBPbUydkqXYtsdNe9LQ2NJGPTbxZByMSW9R/YlPLOUO1xW7arh63zMed2W5u
SJFyBroquRw9vJVRhVYDmNJOzL5o7OClOEPPWgv9Riz4/sCWvgX5vEFuCBT8PsXUNmCe8QUE/wzs
Y+BjnQntyrdsMPPVcRhX6wagdHPgcq8A2lnHnLtwMewfBWT38BiACp5scPHOu+hyB76YJsIMNJtC
25yc/QIDAQAB

* Test scramble_string => 16 chars
XMOx+PZLA15tKvEB
* Test encode_string => 256 chars
�/��2�C���i�5�c�]G�!��Do��Cu]K�ӓ#j.��AW�i�^�_�������������x�����K2�S�&k�t�
��.>���fG9&�\,���e�r�I{�`ee���Ǣ\ɪL�CqԀ�p(� �Q�mbq��0�a�iI(6�Y;,�?�N�ݷHh�bJCp�!��0�����2�Q�����,X�k�X�!'g��W-���/�t^pت`���nK��h�MƐK�
��By�W�{��aV��
* Test encode_string_base64 => 348 chars
bM0ekgWEYIroYPioZ7qZO2iR5L0dfPKfd6pptwHXc+qBqkJd5uIG4BBzFm8I4xVeKXv3Haf/xpx4
3pRVw6FCS8kEWcfevsn8AQX1Pf37eMgLxVP3t0CZ4dPHmNB28AMAJaKr5v5jII+lYrsKqeRjWQ8Z
RFKLfwyxnn9R9TPpaBL0S+QRgNIybp/m6bQ5POBOlvcHer5wtmSGbCTFMXF54ZT90DkpOD/gVGtx
YmLgfEWqKmXjjm+mXMkqPlFKHarJB0A22mA6yKAgrfEi3gjaofbZ6z3SLOR44YKM0RJFHNM5DV/p
qTp2O1pgQI8iHrm+t18vcSzt7lqkhsmBHhpmKQ==
* Test decode_string => 9 chars
BLABLABLA
```
