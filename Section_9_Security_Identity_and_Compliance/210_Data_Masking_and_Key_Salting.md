# 210. Data Masking and Key Salting

Ways to protect **PII** and other sensitive data.

## Masking

**Obfuscates** data, for example showing only the **last 4 digits** of a card or social security number, or stars for a password.

Built in to **Glue DataBrew** and **Redshift**. A Redshift policy that hides a card number completely (knowing it exists matters more than the syntax):

```sql
CREATE MASKING POLICY hide_card_number
WITH (card_number VARCHAR(256))
USING ('XXXX-XXXX-XXXX-XXXX'::TEXT);
```

## Anonymisation

Removes the link between the data and the person.

| Technique | Idea |
|---|---|
| **Replace with random** values | Nothing traces back to the original |
| **Shuffle** | Mix the values of a column, so they no longer match their rows |
| **Encrypt** | **Deterministic:** the same input always gives the same output. **Probabilistic:** it can differ each time |
| **Hash** | Apply a one-way hash function |
| **Delete, or never import** | The safest: drop it in **ETL** or do not collect it |

The lecture suggests hash collisions add to anonymity. With strong hash functions collisions are practically never seen, and the hash of a **guessable value** (such as a card number) can be found by trying all candidates. Hashing alone is weak protection for such data.

## Key salting

*From the course slides.*

A **salt** is a **random value** added to data (often a password) **before hashing**.

`stored hash = SHA-256(password + salt)`

| User | Password | Salt | Stored hash |
|---|---|---|---|
| A | same | salt A | hash 1 |
| B | same | salt B | hash 2 (**different**) |

- Defeats **rainbow tables** (precomputed hashes of common passwords).
- Identical passwords **no longer give identical hashes**.
- Use a **cryptographically secure random** salt, **unique per user**, and **rotate** salts periodically.
- **Salt and hash passwords before storing them.**

Outside the course: real password storage uses a deliberately slow algorithm such as **bcrypt, scrypt or Argon2** rather than plain SHA-256.

## Exam takeaways

1. **Hide part of a value** → **masking** (DataBrew, Redshift).
2. **Not needed** → do not collect it.
3. **Rainbow table** protection → **salting**.
