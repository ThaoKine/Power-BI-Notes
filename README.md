# Big disclaimer:

Everything I write here is not to teach you or anything, because obviously, these are not enough. Therefore, I highly recommend you watch the video of Alex The Analyst (These notes were made while I were watching his tutorials)

[Learn Power BI under 3 hours](https://youtu.be/I0vQ_VLZTWg?si=UEwHmCtvJqR3q-Vm)

# 1. Power BI Interface Navigation
## Load data and transform data in PBI

**Loading data:** move data from a source to another place (in this case is PBI)

**Transforming data: involve doing some editing and changing with Power Query Editor and THEN, it will load the data in PBI** 

>💡 Note with the PBI interface: the report view doesn’t have anything, so click the table view below.
>

# Model view

- It will be useful to have them when you have multiple tables and you want to connect them.

# Exercises

Question 1: where do spend the least amount of money buying the exact same products? ⇒ (easier to identify the cheapest price)

![image](https://github.com/user-attachments/assets/7e0d2dd2-94f8-4511-8b5b-2b7202bc52f6)


Although it shows that we spend the lowest on Costco, but is it the same for EVERY PRODUCT?

![image](https://github.com/user-attachments/assets/1d58665b-4729-47aa-9cd9-6dcb8a892ec1)


Now that we see clearly that not every product at Costco is cheaper than the other supermarkets.

Since the rice and Canned Vegetables at Target are cheaper.

# 2. Power Query
> 💡 Unpivot Columns in Power Query means turning column headers into row values, so your data becomes longer instead of wider — making it easier to analyze.
> 

✅ Use it when you have repeated column names like months, subjects, or categories, and you want them all in **one column** instead.

# 3. Models/Relationships

## 🧠 1. What is a "Relationship" in Power BI?

A **relationship** in Power BI is like a **bridge** that connects two tables so they can "talk to each other."

### 🧩 Imagine this:

You have two tables:

**Students Table**

| StudentID | Name |
| --- | --- |
| 1 | Alice |
| 2 | Bob |

**Scores Table**

| StudentID | Subject | Score |
| --- | --- | --- |
| 1 | Math | 90 |
| 2 | Math | 78 |

👉 Both tables have something in common: **StudentID**.

A **relationship** connects the two tables using that shared column.

---

## 🔍 2. Why Do You Need Relationships?

Without a relationship, Power BI doesn’t know how the tables are related, so it **can’t combine data correctly** in visuals.

With a relationship:

- You can show “Name” from the **Students table** and “Score” from the **Scores table** in the **same chart**.
- Power BI knows **which score belongs to which student**.

---

## ⚙️ 3. How to Create a Relationship in Power BI (Model View)

### 🧭 Step-by-step:

### 🔁 Option 1: Drag-and-Drop (Easiest)

1. Go to **Model view** (click the **3rd icon on the left panel**, shaped like a grid with connections).
2. You’ll see all your tables as boxes.
3. Click and **drag the matching field** (like `StudentID`) from one table and **drop it onto** the same field in the other table.
4. Done! Power BI creates a line (relationship) between them.

### 🔁 Option 2: Manual Method

1. Still in **Model view**, go to the top ribbon and click **“Manage relationships.”**
2. Click **“New”**.
3. Select **Table 1** and the column (e.g., StudentID).
4. Select **Table 2** and the matching column.
5. Click **OK**.

---

## 🔑 4. Things You Should Know

## 🧠 What Is “Cardinality”?

**Cardinality** describes **how many rows** in one table match to **how many rows** in another table when you create a relationship.

## 🔢 1. One-to-One (1:1)

### 🧩 What it means:

Each value in **Table A** matches **only one** value in **Table B**, and vice versa.

| Table A – Employee Info | Table B – Employee Salary |
| --- | --- |
| EmployeeID | Name |
| 1 | Alice |
| 2 | Bob |

👉 Each EmployeeID appears **once** in both tables.

✅ Use **One-to-One** when:

- Both tables have **unique values** in the related columns.
- Each item appears only once in each table.

### 🔹 *One-to-Many* (1:*):

- Most common.
- One table (like Students) has **unique values** (each student only once).
- The other (like Scores) has **repeated values** (multiple scores per student).

---

## 🔢 2. Many-to-One (Many:1) or One-to-Many (1:Many)

These two are actually the **same relationship**, just described from different sides.

### 🧩 Example:

| Table A – Sales (Many Rows) | Table B – Products (One Row Each) |
| --- | --- |
| ProductID | SaleAmount |
| 1 | 50 |
| 1 | 30 |
| 2 | 20 |

👉 In the **Sales table**, **ProductID** appears **many times**.

👉 In the **Products table**, each ProductID appears **only once**.

This is a **Many-to-One** relationship:

- **Many sales** link to **one product**.

✅ Use Many-to-One when:

- One table (like Sales) has **repeated values**.
- The other table (like Products) has **unique values**.

---

## 🎯 Summary Table:

| Type | Meaning | Common Example |
| --- | --- | --- |
| One-to-One | One row matches one row | Employee info + salary |
| One-to-Many | One row matches many rows | Product → Sales |
| Many-to-One | Many rows match one row (same as 1:Many) | Sales → Product |

---

### 🔹 *Direction of Filtering*:

## 🔄 First, What Is “Cross Filter Direction”?

It controls **which table can filter the other** when you use them in charts or slicers.

---

## 🔹 Option 1: **Single** (the default)

- **Only one table** can filter the other.
- Usually, the **"one" side** (the lookup table) filters the **"many" side** (the data table).

### 🧩 Example:

You have:

- `Products table` (1 row per product)
- `Sales table` (many rows per product)

If you choose **Single**:

- When you filter by product name → ✅ it filters the sales.
- But if you filter by something in the **sales table** → ❌ it **won’t** filter the products.

✅ Good for most dashboards. It's **faster and safer**.

---

## 🔁 Option 2: **Both**

- **Both tables can filter each other**.
- So a filter in either table can affect visuals using the other.

### 🧩 Same example:

With **Both**:

- Filter by product name → ✅ filters sales.
- Filter by sales region → ✅ filters the products shown.

✅ Use “Both” when:

- You need **interactions in both directions** (like slicers or multiple lookup tables).
    
    ⚠️ But be careful: it can **slow things down** or cause **loops/conflicts**.
    

---

## 🎯 Summary Table:

| Cross Filter Direction | What it means | Best For |
| --- | --- | --- |
| **Single** | One table filters the other | Simple relationships, default |
| **Both** | Both tables can filter each other | Complex reports with slicers |

> More for you: “Make this relationship active”	= Tells Power BI to use this connection instead of another one between the same tables
> 
---

## 💡 Beginner Tips

- Always make sure the column you’re using to create a relationship has **matching values** in both tables.
- Relationships **don’t duplicate** or change your data. They just allow tables to work together in visuals.
- If Power BI auto-detects a relationship when you load data, check that it's using the **correct fields**!

---

here’s an example of what will it look like:
![image](https://github.com/user-attachments/assets/d37de5f3-2d58-40d6-bb2b-4d6d809aa862)


