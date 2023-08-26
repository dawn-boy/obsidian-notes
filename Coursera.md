## Aim: 
- Secret Key establishment,
- Secure Communication.

## The Triplets:
**K ==> Key,
M ==> Message Text,
C ==> Cipher Text.

## The Duo:
E ==> Encryption Function,
D ==> Decryption Function.

## Definition: 
Since, 
$$ E(K,M) = C $$
and, 
$$ D(K,C) = M $$

Then, Every Cipher must satisfy the below rule.
$$ D(K,E(K,M)) = M$$
## Math behind Decryption:
We know,
$$ D(K,E(K,M)) = M $$
So, 
$$ K \oplus(K \oplus M) = (K \oplus K) \oplus M$$
***
*since anything XORed itself results in zero,***
$$ X \oplus X = 0 $$
*and zero XORed with something results itself,*
$$ 0 \oplus X = X $$
***
We have,
$$ 0 \oplus M = M $$
***
### Onetime pad
This is a really secure cipher with keys as long as the message but transfering those keys are a challenge.

### PRG (Psedorandom generator)
Keys are not as long as the message
This is not real randomness since that randomness is obtained by a seed algorithm 
If prefix has been guessed then the whole cipher text is compromised
