# 🚖 Taxi Cancellation Prediction

## 📌 Overview
YourCabs.com, a taxi company in Bangalore, India, faced a high rate of cancellations by the business due to vehicle unavailability, leading to poor customer experience. This project builds a **predictive model** to classify new bookings as either **likely to be canceled or completed**, enabling proactive interventions.

## 🎯 Business Objective
- **Reduce last-minute cancellations** to improve customer satisfaction.
- **Identify key factors** influencing booking cancellations.
- **Develop a machine learning model** to predict cancellations.
- **Leverage data insights** to optimize fleet allocation and operations.

---

## 📊 Dataset
- **10,000 bookings from 2011-2013**.
- **Target Variable:** `Car_Cancellation` (1 = canceled, 0 = not canceled).
- **Key Features:**
  - **Booking & Travel Details:**
    - `id`: Unique booking ID.
    - `user_id`: Customer identifier.
    - `vehicle_model_id`: Vehicle model type.
    - `travel_type_id`: Type of travel (1 = long distance, 2 = point-to-point, 3 = hourly rental).
    - `package_id`: Type of package booked (1=4hrs & 40kms, 2=8hrs & 80kms, 3=6hrs & 60kms, 4= 10hrs & 100kms, 5=5hrs & 50kms, 6=3hrs & 30kms, 7=12hrs & 120kms)
    - `from_date`, `to_date`: Trip start and end timestamps.
    - `booking_created`: Timestamp of when the booking was made.
  - **Booking Method:**
    - `online_booking`: Whether booking was done via desktop website.
    - `mobile_site_booking`: Whether booking was done via mobile website.
  - **Geographic Information:**
    - `from_area_id`, `to_area_id`: Unique area identifiers for trip locations.
    - `from_city_id`, `to_city_id`: City identifiers for intercity travel.
    - `from_lat`, `from_long`: Latitude and longitude of the pickup area.
    - `to_lat`, `to_long`: Latitude and longitude of the drop-off area.
  - **Handling Missing Values:**
    - Imputed missing values using appropriate statistical techniques.
    - Applied one-hot encoding for categorical variables.

---

## 🤖 Model Development
### **📌 Machine Learning Pipeline**
1. **Data Preprocessing**
   - Dropped irrelevant/missing columns.
   - Scaled numerical features using `StandardScaler`.
   - Applied **imputation techniques** to handle missing values.
   - Performed **one-hot encoding** for categorical variables.
2. **Feature Engineering**
   - Created `distance` (derived from latitude and longitude values).
   - Derived `booking_lead_time` (difference between booking time and trip start time).
   - Extracted `trip_duration` (difference between start and end time).
   - Categorized `booking_created` and `from_date` into **session of the day** (morning, afternoon, evening, night).
   - Marked bookings as `weekday/weekend` based on booking and trip start times.
   - Categorized `from_area_id` into different levels of cancellation risk.
3. **Model Training**
   - **Support Vector Machine (SVM) with RBF Kernel** (initial baseline model).
   - **Decision Tree Classifier** to compare performance.
4. **Hyperparameter Tuning**
   - Tuned model parameters using **GridSearchCV** to optimize performance.
   - Applied cross-validation to ensure stability.
5. **Model Evaluation**
   - **Baseline Accuracy:**
     - **SVM:** 93.1%
     - **Decision Tree:** 87.85%
   - **Cross-Validation Accuracy & Standard Deviation:**
     - **SVM:** 92.66% ± 0.22
     - **Decision Tree:** 88.39% ± 0.70
   - **After Hyperparameter Tuning:**
     - **SVM:** 93.25%
     - **Decision Tree:** 93.15%
   - **ROC-AUC Scores:**
     - **SVM:** 0.70
     - **Decision Tree:** 0.77
   - **Conclusion:** While both models performed well, the Decision Tree model had a better ROC-AUC score, making it a more practical choice.

---

## 📈 Business Takeaways
Predictive modeling for ride cancellations has several real-world applications beyond traditional taxi services. The insights derived from this project can be extended to:
- **Fleet Optimization**: Ensuring better vehicle availability by forecasting peak demand times and potential cancellation risks.
- **Rideshare and Mobility Platforms**: Companies can utilize similar models to improve driver allocation and reduce ride rejections.
- **Public Transportation and Logistics**: Predictive analytics can help in optimizing routes and ensuring availability in transport networks.
- **Customer Retention Strategies**: Understanding frequent cancellation patterns can help implement customer engagement strategies and incentive-based retention.
- **Autonomous Vehicle Fleet Management**: Self-driving car services can use cancellation prediction to optimize fleet dispatch and minimize inefficiencies.

By leveraging these predictive insights, companies can enhance operational efficiency, reduce downtime, and improve overall customer experience.
