##### JWT Integration
```
1. Always check what library they are using first.
2. Always check what method they are using to decode and verify the JWT.

In the example below the jsonwebtoken library is used.
The jwt.decode method is used to decode the token.
The jwt.verify method is not used to verify the token.
```
![[Pasted image 20240731095911.png]]