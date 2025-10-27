AWS Database migration Service (DMS) is a managed service that help you migrate and replicate databases from one source to another with minimal downtime.

https://www.youtube.com/watch?v=YVIugsV6egQ

---

### 🧭 **Step-by-Step Process in AWS DMS**

#### **1. Pre-Migration Preparation**

- **Assess the source database**: Identify size, schema, dependencies, and compatibility with the target (Aurora MySQL in your case).
    
- **Create IAM roles**:
    
    - One for DMS to access migration resources.
        
    - One for CloudWatch logging and monitoring.
        
- **Set up networking**: Ensure the **DMS replication instance** can connect to both the source (on-prem DB) and target (Aurora).
    
    - Use **VPN or Direct Connect** for secure connectivity.
        
- **Enable binary logging** (for MySQL sources) to support CDC (Change Data Capture).
    

---

#### **2. Create a Replication Instance**

- Launch a **DMS Replication Instance** in AWS.
    
- It acts as a bridge that reads data from the source and writes to the target.
    
- Choose instance size based on data volume and migration type (full load or full + ongoing replication).
    

---

#### **3. Configure Source and Target Endpoints**

- Define **Source Endpoint** (e.g., on-prem MySQL).
    
    - Provide hostname, port, username, and password.
        
- Define **Target Endpoint** (e.g., Aurora MySQL).
    
    - Provide connection details and credentials.
        
- **Test connections** to ensure connectivity between DMS, source, and target.
    

---

#### **4. Create a Migration Task**

- Specify the **type of migration**:
    
    - **Full Load only** – one-time migration of existing data.
        
    - **Full Load + CDC** – migrate existing data and keep replicating ongoing changes.
        
    - **CDC only** – replicate changes only.
        
- Choose which tables, schemas, or databases to migrate.
    
- Map tables (optional: transform schema names, filter tables, rename columns).
    

---

#### **5. Run and Monitor the Task**

- Start the task — DMS begins migrating data.
    
- Monitor progress in the **AWS DMS console**.
    
    - Check metrics like latency, throughput, and errors.
        
    - Logs are available in **CloudWatch**.
        

---

#### **6. Validate Data**

- Compare record counts, checksums, or sample queries between source and target.
    
- AWS DMS doesn’t automatically validate data, so manual or custom validation scripts are used.
    

---

#### **7. Perform Cutover**

- Stop application writes to the old database.
    
- Allow DMS to apply the last set of changes.
    
- Switch application connections to the Aurora endpoint.
    
- Decommission the on-prem DB after validation.
    

---

#### **8. Post-Migration Optimization**

- Analyze performance on Aurora.
    
- Tune indexes, queries, and connection settings.
    
- Review CloudWatch metrics and cost optimization.
    

---

✅ **Summary Table**

|Step|Task|Key Tools|
|---|---|---|
|1|Preparation|IAM, Networking, Binlog|
|2|Create Replication Instance|AWS DMS|
|3|Define Endpoints|Source & Target DBs|
|4|Create Migration Task|DMS Console|
|5|Run & Monitor|CloudWatch, DMS Dashboard|
|6|Validate Data|SQL Scripts / Tools|
|7|Cutover|Aurora Endpoint|
|8|Post-Migration Tuning|CloudWatch, Performance Insights|