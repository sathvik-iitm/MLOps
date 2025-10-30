# Week 3 Assignment: Feast Feature Store Integration with IRIS Pipeline

## 👨‍💻 Student Information
- **Course:** MLOps
- **Assignment:** Week 3 - Feast Feature Store Integration
- **Date:** October 30, 2025

---

## 🎯 Assignment Objective

Incorporate Feast Feature Store into the existing IRIS ML pipeline to demonstrate:
- Centralized feature management
- Historical feature retrieval for training
- Real-time feature serving for inference
- Integration with Google Cloud Storage (GCS)

---

## 🏗️ Architecture Overview
```
IRIS Dataset (CSV) 
    ↓
Convert to Parquet
    ↓
Feast Feature Store
    ├── Registry (GCS: gs://corded-forge-475015-k6-bucket/feast/)
    ├── Offline Store (Parquet files)
    └── Online Store (SQLite)
    ↓
ML Pipeline
    ├── Training (Historical Features)
    └── Inference (Real-time Features)
```

---

## 📊 Dataset Information

**Source:** Time-aware IRIS dataset adapted for Feast
- **Entities:** 3 iris plants (IDs: 1001, 1002, 1003)
- **Features:** sepal_length, sepal_width, petal_length, petal_width, species
- **Timestamps:** 15 days of data per plant (Sept 17 - Oct 1, 2025)
- **Total Samples:** 45 rows

---

## 🛠️ Implementation Steps

### 1. Environment Setup
- Installed Feast SDK (v0.56.0) with GCP dependencies
- Configured Vertex AI Workbench instance
- Set up GCS bucket for registry storage

### 2. Feature Store Configuration
- **Project Name:** iris_feature_store
- **Registry Location:** GCS (gs://corded-forge-475015-k6-bucket/feast/registry.db)
- **Online Store:** SQLite (local)
- **Offline Store:** File-based (Parquet)

### 3. Feature Definitions
```python
Entity: iris_id (INT64)
Data Source: iris_data_adapted_for_feast.parquet
Feature View: iris_features
  - sepal_length (Float32)
  - sepal_width (Float32)
  - petal_length (Float32)
  - petal_width (Float32)
  - species (String)
```

### 4. Feature Materialization
- Converted CSV to Parquet format
- Materialized 45 samples to online store
- Date range: 2025-09-17 to 2025-10-02

### 5. Model Training
- Algorithm: Decision Tree Classifier
- Training samples: 31
- Test samples: 14
- **Accuracy: 71.4%**

### 6. Real-time Inference
- Fetched features from online store
- Made predictions for 3 iris plants
- Successfully demonstrated end-to-end pipeline

---

## 📁 Project Structure
```
feast_iris_project/
├── iris_feature_store/
│   ├── feature_store.yaml          # Feast configuration
│   ├── feature_repo/
│   │   └── feature_repo.py         # Feature definitions
│   ├── iris_data_adapted_for_feast.csv      # Original data
│   ├── iris_data_adapted_for_feast.parquet  # Converted data
│   ├── iris_feast_model.joblib     # Trained model
│   └── data/
│       └── online_store.db         # SQLite online store
└── week3_feast_integration.ipynb   # Main notebook
```

---

## 🔑 Key Technologies Used

- **Feast:** Feature store framework (v0.56.0)
- **Google Cloud Storage:** Registry storage
- **SQLite:** Online feature store
- **Parquet:** Efficient data format
- **Scikit-learn:** ML model training
- **Pandas:** Data manipulation
- **Vertex AI Workbench:** Development environment

---

## 🎯 Results Achieved

✅ Successfully set up Feast with GCS integration  
✅ Defined entities and feature views  
✅ Materialized features to online store  
✅ Trained model using historical features (71.4% accuracy)  
✅ Implemented real-time inference with online features  
✅ Registry stored in GCS for production use  

---

## 🚧 Challenges Encountered & Solutions

### Challenge 1: Registry Type Configuration
**Error:** `FeastRegistryTypeInvalidError: Feature server type was set to gcs`
**Solution:** Changed from `registry_type: gcs` to direct path: `registry: gs://bucket/path/`

### Challenge 2: File Format Compatibility
**Error:** Feast expected Parquet but CSV was provided
**Solution:** Converted CSV to Parquet format using pandas

### Challenge 3: Entity ValueType
**Error:** Deprecation warning about missing value_type
**Solution:** Added `value_type=ValueType.INT64` to entity definition

---

## 📚 Key Learnings

1. **Feature Store Benefits:** Centralized feature management prevents inconsistencies between training and serving
2. **Time-Aware Features:** Feast's point-in-time joins prevent data leakage
3. **Online vs Offline Stores:** Different stores optimized for different use cases
4. **GCS Integration:** Production-ready setup with cloud storage for registry

---

## 🔮 Future Enhancements

- Integrate BigQuery as offline store for larger datasets
- Add feature transformations (on-demand feature views)
- Implement feature monitoring and drift detection
- Set up CI/CD pipeline for feature definitions
- Add more sophisticated ML models

---

## 📞 References

- [Feast Documentation](https://docs.feast.dev/)
- [GCP Vertex AI](https://cloud.google.com/vertex-ai)
- [Scikit-learn Documentation](https://scikit-learn.org/)

---

## ✅ Conclusion

Successfully implemented Feast Feature Store into the IRIS ML pipeline, demonstrating:
- Production-ready feature management
- Integration with GCP services
- End-to-end ML workflow with feature store
- Real-time feature serving capabilities

The assignment objectives have been fully met with a working implementation deployed on GCP.
