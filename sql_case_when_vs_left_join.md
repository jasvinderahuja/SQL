# SQL: CASE WHEN vs LEFT JOIN

Today we added a new `specialty_type`, and I stumbled upon an old SQL view with a structure like this:

```sql
CASE WHEN dept = 'dept_A' AND specialty_type = 'sp_A' AND degree = 'deg_A' THEN 'a'
     WHEN dept = 'dept_B' AND specialty_type = 'sp_B' AND education = 'deg_B' THEN 'b'
     ...
     -- over 100 lines of hardcoded conditions
END AS code
```

If you've ever seen or written something like this, here's a recommendation:  
## Don't embed business logic like this directly in your SQL.  

Instead, create a **mapping table**:

| dept   | specialty_type | education | code |
|--------|----------------|-----------|------|
| dept_A | sp_A           | deg_A     | a    |
| dept_B | sp_B           | deg_B     | b    |
| ...    | ...            | ...       | ...  |

Then simply `LEFT JOIN` it in your query.

## Why this is better:
- Easy to maintain and scale  
- No need to touch the view for new logic — just add a row  
- Business rules are stored as data, not buried in code

It’s a small change that saves a lot of pain in the long run.

#SQL #DataEngineering #BestPractices #CleanCode
