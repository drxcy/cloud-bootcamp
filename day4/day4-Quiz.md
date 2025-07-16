# 📋 Day 5 – AWS Storage Quiz ✅

---

### 1. ❓ What type of storage is Amazon S3?

**Answer:** Object storage  
> Stores files as objects inside buckets (ideal for backups, images, logs)

---

### 2. ❓ Can you install software directly on S3?

**Answer:** No  
> S3 is not a compute service. You store static files, not run programs.

---

### 3. ❓ What is the difference between EBS and S3?

| Feature | EBS | S3 |
|--------|-----|----|
| Type | Block storage | Object storage |
| Used for | Attaching to EC2 | Uploading files, backups |
| Mountable | Yes | No |

---

### 4. ❓ What is the maximum size of an S3 object?

**Answer:** 5 TB

---

### 5. ❓ What does S3 versioning do?

**Answer:** Keeps all versions of an object, even if it's overwritten or deleted

---

### 6. ❓ What is the purpose of Amazon Glacier?

**Answer:** Low-cost, archival storage for data rarely accessed

---

### 7. ❓ Can you directly access Glacier like S3?

**Answer:** No  
> You must retrieve the data through restore, which takes minutes to hours.

---

### 8. ❓ What is a lifecycle rule in S3?

**Answer:** Automation that transitions data to cheaper storage classes (like Glacier) or deletes it after a certain period.

---

### 9. ❓ Which EBS volume type is most commonly used?

**Answer:** gp3 (General Purpose SSD)

---

### 10. ❓ Can EBS volumes be moved between AZs?

**Answer:** No  
> EBS volumes are **AZ-bound**. You must create a snapshot and restore it in a different AZ.

---
