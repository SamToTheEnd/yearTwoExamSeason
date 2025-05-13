# Relational Algebra Examples

## Database Schema

We have three tables:

### Students
| student_id | name    |
|------------|---------|
| 1          | Sam     |
| 2          | Seoyeon |
| 3          | Alan    |

### Degrees
| degree_id | degree_name      |
|-----------|------------------|
| 101       | InfoSec          |
| 102       | Music            |
| 103       | Computer Science |

### Enrollments
| student_id | degree_id | module_name    |
|------------|-----------|----------------|
| 1          | 101       | Cryptography   |
| 1          | 103       | Programming    |
| 2          | 102       | Song Writing   |
| 2          | 103       | Programming    |
| 3          | 101       | Cryptography   |
| 3          | 103       | Programming    |

## Sample Relational Algebra Queries

### 1. Selection (σ)
**Query**: Find all students named "Sam"
```
σ(name = "Sam")(Students)
```

**Result**:
| student_id | name |
|------------|------|
| 1          | Sam  |

### 2. Projection (π)
**Query**: List all module names
```
π(module_name)(Enrollments)
```

**Result**:
| module_name  |
|--------------|
| Cryptography |
| Programming  |
| Song Writing |

### 3. Natural Join (⋈)
**Query**: Join Students and Enrollments to see which student is taking which module
```
Students ⋈ Enrollments
```

**Result**:
| student_id | name    | degree_id | module_name    |
|------------|---------|-----------|----------------|
| 1          | Sam     | 101       | Cryptography   |
| 1          | Sam     | 103       | Programming    |
| 2          | Seoyeon | 102       | Song Writing   |
| 2          | Seoyeon | 103       | Programming    |
| 3          | Alan    | 101       | Cryptography   |
| 3          | Alan    | 103       | Programming    |

### 4. Join with Condition (⋈condition)
**Query**: Find all InfoSec students and their modules
```
Students ⋈ Enrollments ⋈(degree_id = 101) Degrees
```

**Result**:
| student_id | name | degree_id | module_name  | degree_name |
|------------|------|-----------|--------------|-------------|
| 1          | Sam  | 101       | Cryptography | InfoSec     |
| 3          | Alan | 101       | Cryptography | InfoSec     |

### 5. Cartesian Product (×)
**Query**: Generate all possible combinations of students and degrees
```
Students × Degrees
```

**Result** (partial):
| student_id | name    | degree_id | degree_name      |
|------------|---------|-----------|------------------|
| 1          | Sam     | 101       | InfoSec          |
| 1          | Sam     | 102       | Music            |
| 1          | Sam     | 103       | Computer Science |
| 2          | Seoyeon | 101       | InfoSec          |
| ...        | ...     | ...       | ...              |

### 6. Set Difference (-)
**Query**: Find students who study Programming but not Cryptography
```
π(student_id)(σ(module_name = "Programming")(Enrollments)) - π(student_id)(σ(module_name = "Cryptography")(Enrollments))
```

**Result**:
| student_id |
|------------|
| 2          |

### 7. Intersection (∩)
**Query**: Find students who are enrolled in both Computer Science and InfoSec
```
π(student_id)(σ(degree_id = 103)(Enrollments)) ∩ π(student_id)(σ(degree_id = 101)(Enrollments))
```

**Result**:
| student_id |
|------------|
| 1          |
| 3          |

### 8. Union (∪)
**Query**: Find all students taking either Cryptography or Song Writing
```
π(student_id)(σ(module_name = "Cryptography")(Enrollments)) ∪ π(student_id)(σ(module_name = "Song Writing")(Enrollments))
```

**Result**:
| student_id |
|------------|
| 1          |
| 2          |
| 3          |