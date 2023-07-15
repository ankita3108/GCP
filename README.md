# Credit Card Fraud Detection Using GCP
This project aims to develop a comprehensive credit card fraud detection system for Transpe Limited, a global transaction company responsible for handling transactions across multiple banks worldwide. The system utilizes historical financial and demographic data to train a machine learning model, deploys it on Vertex AI Endpoint for real-time transaction analysis, and incorporates various components to process, classify, and handle fraudulent transactions. Additionally, Looker Dashboards are created to provide detailed insights into both fraud and non-fraud transactions, enabling effective monitoring and analysis.

## Toolbox 🧰
<img src="https://miro.medium.com/v2/resize:fit:335/0*ARUQelkPpC1LwNFN" width="200" height="120" alt="Pub Sub"/> &emsp; <img src="https://lh6.googleusercontent.com/1MICxjbrbRPtEnzE54g2shaMRD2RocCIcuSOrqwaqryObCR6IrsXNb3Sd5MjBBwmoLeVcgVu_SE3vw-IbRA24SFhH4IT1xppVuuNGodDtFEykgD0Cw1vB2jITTsOgBNHvWfw27icmMs30SYgWQ" width="200" alt="GCP DTAFLOW" height="70"/>
&emsp; <img src="https://miro.medium.com/max/600/1*HEzofakm1-c4c_Qn4zjmnQ.jpeg" width ="170" height="75" alt="Apache Beam"/>
&emsp;<img src ="https://i.ytimg.com/vi/s6ytxB0YSR0/mqdefault.jpg" width="170" height="70" alt="Secret Manager"/> &emsp;
<img src ="https://th.bing.com/th/id/OIP.k11NKB6vQbDyHstjaXOJygHaCk?pid=ImgDet&rs=1" width="200" height="100" alt="Google Cloud Storage"/> &emsp;
<img src ="https://cxl.com/wp-content/uploads/2019/10/google-bigquery-logo-1.png" width="170" height="100" alt="Google Big Query"/> &emsp;
<img src ="https://miro.medium.com/v2/resize:fit:584/1*q4EVSAndlvgFLyR6ncc4Bg.png" width="170" height="100" alt="Google cloud Functions"/> &emsp;
<img src ="https://assets.website-files.com/618399cd49d125734c8dec95/63905b4ecedc3f60172bcd63_vertexai.png" width="170" height="100" alt="Vertex AI"/> &emsp;
<img src ="https://res.cloudinary.com/hevo/image/upload/f_auto,q_auto/v1685918308/hevo-learn-1/Firestore-Data-Model-firestore-logo.png?_i=AA" width="170" height="100" alt="Google cloud Firestore"/> &emsp;
<img src ="https://miro.medium.com/v2/resize:fit:961/1*tQKERQdZsjUArxXjaHo9PA.png" width="170" height="100" alt="Secret Manager"/> &emsp;
<img src ="https://logos-world.net/wp-content/uploads/2022/02/ServiceNow-Symbol.png" width="100" height="100" alt="ServiceNow"/> &emsp;
<img src ="https://i.pinimg.com/originals/8d/39/f3/8d39f3958e82028615cdedacb496a114.jpg" width="170" height="100" alt="SMTP"/> &emsp;
<img src ="https://www.python.org/static/community_logos/python-logo-master-v3-TM-flattened.png" width="170" height="100" alt="Python"/> &emsp;

## Architecture Diagram

<img src ="https://github.com/sandy0298/Credit_card_Fraud_Detection_uisng_GCP/blob/main/screenshots/arch.png" width="900" height="700" alt="architecture"/> &emsp;

## Project Workflow:

## Key Steps:

## 1. Data Preparation:
   - The project utilizes existing historical financial and demographic data generated by Transpe Limited, which is stored in BigQuery.
   - This data serves as the foundation for training the credit card fraud detection model.
   - BigQuery ML (BQML) is leveraged to perform feature engineering, data transformation, and model training.

## 2. Model Deployment:
   - Once the model is trained, it is deployed and pushed to the Vertex AI Endpoint.
   - The deployed model enables real-time prediction of transaction records, allowing immediate fraud detection.

## 3. Real-time Transaction Processing:
   - Real-time transaction data originating from on-prem servers flows into a Pub/Sub topic.
   - The Pub/Sub topic serves as a centralized data stream for the subsequent processing steps.

## 4. Stream Processing and Database Storage:
   - A streaming Dataflow pipeline is implemented to continuously pull transaction records from the Pub/Sub subscriber.
   - Each transaction record is processed and loaded into a Firestore database for efficient storage and retrieval.
   - The database provides a scalable and reliable storage solution for the incoming transaction data.

## 5. Fraud Detection and Classification:
   - Each transaction record received by the streaming pipeline is sent to the Vertex AI Endpoint for prediction.
   - The deployed machine learning model analyzes the transaction features and assigns a fraud likelihood score.
   - The model's output includes a "predicted_isFraud" column, which indicates the probability of the transaction being fraudulent.

## 6. Data Storage and Analysis:
   - Based on the fraud prediction results, the transaction records are written to specific BigQuery tables:
     - If the "predicted_isFraud" column is 0, indicating a non-fraudulent transaction, the record is stored in the "non_fraud_transaction" table.
     - If the "predicted_isFraud" column is 1, indicating a fraudulent transaction, the record is stored in the "fraud_transaction_layer" table.

## 7. Fraud Alert and Incident Handling:
   - For transactions identified as fraudulent, a separate Pub/Sub topic is utilized to manage the events.
   - When a fraud transaction is detected, a triggered cloud function is executed to handle various actions:
     - The function sends email alerts to the affected customers, notifying them of the fraudulent activity.
     - Email notifications are also sent to the sender's bank, providing visibility into the fraudulent transaction.
     - The cloud function creates a high-priority incident ticket on the Transpe side, ensuring immediate attention and resolution.
   - The necessary credentials required for email alerts and incident ticket creation are fetched securely from the Secret Manager.

## 8. Looker Dashboards:
   - Looker Dashboards are created to provide comprehensive visualizations and insights into the fraud detection system.
   - Separate dashboards are designed for fraud and non-fraud transactions, offering detailed analytics, trends, and key performance indicators.
   - The dashboards empower Transpe's analysts and stakeholders to monitor transaction activities, identify patterns, and make informed decisions.

## Conclusion:

The credit card fraud detection system developed for Transpe Limited combines machine learning, stream processing, cloud infrastructure, and automated alerts to proactively identify and handle fraudulent transactions. By leveraging historical data, real-time prediction models, and advanced analytics, Transpe enhances security, protects customers, and reduces financial risks associated with credit card fraud. The incorporation of Looker Dashboards further enables efficient monitoring and analysis of transaction data, empowering Transpe to stay ahead in the fight against fraudulent activities.

## Data reference : 

https://lnkd.in/dHWktGf3

## Dashboard

<img src = "https://github.com/sandy0298/Credit_card_Fraud_Detection_uisng_GCP/blob/main/screenshots/Screenshot%20(18).png" width="800" height="600" alt="report1"/> &emsp;
<img src ="https://github.com/sandy0298/Credit_card_Fraud_Detection_uisng_GCP/blob/main/screenshots/Screenshot%20(19).png" width="800" height="600" alt="report2"/> &emsp;
<img src ="https://github.com/sandy0298/Credit_card_Fraud_Detection_uisng_GCP/blob/main/screenshots/Screenshot%20(20).png" width="800" height="600" alt="report2"/> &emsp;
## servicenow Dashboard

<img src ="https://github.com/sandy0298/Credit_card_Fraud_Detection_uisng_GCP/blob/main/screenshots/servicenow.png" width="800" height="600" alt="report2"/> &emsp;

## Email to Bank
<img src ="https://github.com/sandy0298/Credit_card_Fraud_Detection_uisng_GCP/blob/main/screenshots/bank.png" width="800" height="600" alt="report2"/> &emsp;

## Email to Customer
<img src ="https://github.com/sandy0298/Credit_card_Fraud_Detection_uisng_GCP/blob/main/screenshots/customer.png" width="800" height="600" alt="report2"/> &emsp;


## Link to Dashboard

## Fraud data dashboard

https://lookerstudio.google.com/reporting/c2f9bdb7-b3f2-4f0e-9c8f-aec29b999248

## Non-Fraud Data Dashboard
https://lookerstudio.google.com/reporting/91c4bff5-7ec0-4149-8095-3acba2cfa0f6
### Code structure
```
├── Home Directory
|     ├── Transaction_pubsub.py
|     ├── Transaction_Pipeline.py
├── setup.py
 
```
## Installation Steps and deployment process

## 1. Run the streaming dataflow Pipeline (datastream_ingestion.py):
   a. Start the dataflow_ingestion.py script, which initiates the streaming dataflow pipeline.
   b. The pipeline is designed to continuously pull data from a pub/sub subscriber.
   c. The pulled data is then stored in Firestore, a NoSQL document database.
   d. Within the pipeline, various operations can be performed on the data, including predictions using machine learning models or any other required transformations.

## 2. Load transaction records to pub/sub (transaction_pubsub.py):
   a. Execute the transaction_pubsub.py script to load transaction records into a pub/sub topic.
   b. This script ensures that new transaction records are continuously published to the specified pub/sub topic in real-time.
   c. These records will be processed by downstream components, such as the streaming dataflow pipeline.

## 3. Trigger cloud function on fraud record from pub/sub:
   a. Deploy a cloud function that is designed to trigger when a fraud record is detected within the pub/sub topic.
   b. Configure the cloud function to listen to the specific pub/sub topic where the fraud records are published.
   c. When a new fraud record is detected, the cloud function is triggered automatically.
   d. The cloud function can then execute custom logic, such as sending email notifications or creating ServiceNow tickets based on the detected fraud.

## 4. Create email notifications and ServiceNow tickets:
   a. Within the cloud function triggered by the fraud record, include the necessary code to send email notifications.
   b. Utilize appropriate email sending APIs or services to compose and send the notifications to relevant customers and banks.
   c. Similarly, within the cloud function, integrate with the ServiceNow API to create new tickets based on the fraud record.
   d. Provide the required details and fields to create a new ticket with relevant information about the fraud incident.
   e. Ensure proper error handling and logging mechanisms are in place to track the status and outcomes of the email notifications and ServiceNow ticket creation.

These steps outline the process of deploying and running the necessary components to handle the streaming dataflow pipeline, pub/sub integration, fraud detection triggering, and subsequent email notifications and ServiceNow ticket creation.
