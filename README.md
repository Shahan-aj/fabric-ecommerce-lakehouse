# E-commerce Lakehouse on Microsoft Fabric (Medallion Architecture)

End-to-end **Medallion Architecture (Bronze → Silver → Gold)** implemented in **Microsoft Fabric** using **Delta Lake + PySpark**, with a **Power BI semantic model** for analytics.

![Partitioning](images/partition_fabric.png)

## ✨ Key Features
- **Incremental ingestion** with `Modified_TS` watermarking
- **Delta tables** (ACID, MERGE/UPDATE/DELETE, time travel)
- **Partitioned layout** for performance: `/Files/Bronze/Sales/Order_Year=YYYY/Order_Month=MM/`
- **Star schema** in Gold: `Fact_Sales` + dimensions (Product, Customer, ShipMode, OrderPriority, OrderReturn, Date)
- **Idempotent upserts** using Delta `MERGE`
- **Power BI** model & relationships on top of Gold

## 🪙 Medallion Layers (short)
**Bronze – Raw**  
Excel landing in OneLake → standardized → **partitioned Delta** → **incremental** by watermark.

**Silver – Transform**  
Cleansing, derived fields (`Order_Year`, `Order_Month`, `Aging`), de-dupe, business rules.

**Gold – Model**  
Star schema + semantic relationships; MERGE-based upserts for dimensions, append/merge for facts.

![Semantic Model](images/semantic_model_fabric.png)

## 🧱 Tech Stack
- Microsoft **Fabric** (Lakehouse, Notebooks, Pipelines/Dataflow Gen2)
- **PySpark / Spark SQL**
- **Delta Lake** on OneLake
- **Power BI** (Semantic model + report)

## 📂 Project Structure
