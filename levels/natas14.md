# Natas 14: SQL injection (auth bypass)

**Vulnerability:** user input concatenated directly into a SQL query.

The login query concatenates the username and password straight into the SQL string. A classic injection in the username field closes the quote, forces a condition that is always true, and comments out the rest of the query (including the password check):

```sql
" OR 1=1 -- -
```

The login succeeds and the page returns the password.

**Password:** `<natas15 password>`

[← Natas 13](natas13.md) · [Next: Natas 15 →](natas15.md)
