# ID verification

> `IDCardUtils` is mainly used to verify the correctness of the Chinese resident ID card in **local**, the usage method is as follows:

```kotlin
IDCardValidate("123456789101112131")
```

Here is a list of cases where validation fails:

1️⃣ The length of the ID card number is not 15 or 18 digits.

2️⃣ The 15-digit number of the ID card is not all numbers; the 18-digit number is not all numbers except the last one.

3️⃣ ID card birthday is invalid.

4️⃣ The birthday of the ID card is not valid.

5️⃣ The ID card month is invalid.

6️⃣ The ID card date is invalid.

7️⃣ The area code of the ID card is wrong.
