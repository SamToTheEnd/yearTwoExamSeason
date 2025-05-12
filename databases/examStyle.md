


## Serialisability, a sechdule is Serialisability if it is equivilant to a serial schedule (a schedule where transactions are done one after another(in a linear way ))

### Transations should stay within their memeory space, so if you read  and write a in T1, you can not  do it in t2. 

### It shoudl be atomic. So all read and write of B should be either above or blow that of t A.