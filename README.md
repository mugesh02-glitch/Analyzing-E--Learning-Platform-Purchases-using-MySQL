# Analyzing E-Learning Platform Purchases Using MySQL

## Project Overview

This project uses MySQL to analyze purchase data from an online e-learning platform. The database contains information about learners, courses, and purchases. SQL queries are used to generate business insights related to learner engagement, course demand, and revenue generation.

---

## Domain

E-Learning Analytics / Sales Analytics

---

## Business Problem

E-learning platforms need to understand learner behavior, identify popular courses, measure revenue performance, and improve underperforming course offerings.

---

## Objectives

- Store learner, course, and purchase data.
- Create relationships using primary and foreign keys.
- Perform SQL analysis using joins and aggregation.
- Generate business insights from purchase transactions.

---

# Database Creation

```sql
CREATE DATABASE e_learning;
USE e_learning;
```

---

# Create Learners Table

```sql
CREATE TABLE learners (
    learner_id INT PRIMARY KEY,
    learner_name VARCHAR(100),
    email VARCHAR(100),
    city VARCHAR(50)
);
```

---

# Create Courses Table

```sql
CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2)
);
```

---

# Create Purchases Table

```sql
CREATE TABLE purchases (
    purchase_id INT PRIMARY KEY,
    learner_id INT,
    course_id INT,
    purchase_date DATE,
    FOREIGN KEY (learner_id)
        REFERENCES learners(learner_id),
    FOREIGN KEY (course_id)
        REFERENCES courses(course_id)
);
```

---

# Insert Sample Data

```sql
INSERT INTO learners VALUES
(1,'Arun','arun@gmail.com','Chennai'),
(2,'Priya','priya@gmail.com','Coimbatore'),
(3,'Rahul','rahul@gmail.com','Madurai');
```

```sql
INSERT INTO courses VALUES
(101,'Python Programming','Programming',2999),
(102,'Data Analytics','Analytics',3999),
(103,'AI Fundamentals','Artificial Intelligence',4999);
```

```sql
INSERT INTO purchases VALUES
(1,1,101,'2025-01-10'),
(2,2,102,'2025-01-15'),
(3,3,103,'2025-01-20');
```

---

# Display All Learners

```sql
SELECT * FROM learners;
```

---

# Display All Courses

```sql
SELECT * FROM courses;
```

---

# Display All Purchases

```sql
SELECT * FROM purchases;
```

---

# Join Query

Display learner purchase details.

```sql
SELECT
l.learner_name,
c.course_name,
c.category,
c.price,
p.purchase_date
FROM purchases p
JOIN learners l
ON p.learner_id = l.learner_id
JOIN courses c
ON p.course_id = c.course_id;
```

---

# Total Spending by Learners

```sql
SELECT
l.learner_name,
SUM(c.price) AS total_spending
FROM purchases p
JOIN learners l
ON p.learner_id = l.learner_id
JOIN courses c
ON p.course_id = c.course_id
GROUP BY l.learner_name;
```

---

# Revenue by Course Category

```sql
SELECT
c.category,
SUM(c.price) AS total_revenue
FROM purchases p
JOIN courses c
ON p.course_id = c.course_id
GROUP BY c.category;
```

---

# Most Popular Courses

```sql
SELECT
c.course_name,
COUNT(*) AS enrollments
FROM purchases p
JOIN courses c
ON p.course_id = c.course_id
GROUP BY c.course_name
ORDER BY enrollments DESC;
```

---

# Courses Without Purchases

```sql
SELECT
c.course_name
FROM courses c
LEFT JOIN purchases p
ON c.course_id = p.course_id
WHERE p.purchase_id IS NULL;
```

---

# Key Insights

- Data Analytics and AI courses generate strong revenue.
- Learners often purchase courses from multiple categories.
- Some courses receive no enrollments and require improvement.
- Tracking learner spending supports better marketing decisions.

---

# Expected Outcome

- Understand learner purchasing behavior.
- Measure course performance.
- Improve course recommendations.
- Increase revenue through data-driven strategies.

---

# Conclusion

This project demonstrates how SQL can transform raw transactional data into meaningful business insights. Using joins, filtering, aggregation, and reporting techniques, the e-learning platform can optimize course offerings and improve business performance.

---

## Author

**Mugesh Kumar M**

### Project
Analyzing E-Learning Platform Purchases Using MySQL****
