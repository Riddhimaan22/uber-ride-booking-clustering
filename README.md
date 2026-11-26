# Uber Ride Booking Analysis – Temporal Clustering

A Data Mining and Machine Learning project that analyzes temporal patterns in Uber ride bookings using three clustering algorithms: **K-Means, DBSCAN, and Agglomerative Clustering**.

## Project Objective

The objective is to identify meaningful temporal patterns in ride bookings and understand how booking demand varies throughout the day.

The project focuses on grouping individual bookings based on their time of occurrence to identify periods such as late night, early morning, morning, afternoon, evening, and night.

## Dataset

The dataset contains 150,000 Uber ride-booking records and 21 attributes, including:

- Booking date and time
- Booking status
- Vehicle type
- Pickup and drop locations
- Ride distance and booking value
- Customer and driver ratings
- Cancellation information

The primary experiment uses booking date and time. Other attributes are not used in the temporal clustering models.

## Methodology

### 1. Exploratory Data Analysis

- Dataset inspection and missing-value analysis
- Hourly booking distribution
- Daily booking distribution
- Hour versus day-of-week heatmap
- Weekday versus weekend comparison

### 2. Feature Engineering

Booking date and time are combined into a timestamp. Fractional hours are extracted and transformed using cyclical encoding:

\[
Hour\_Sin = \sin(2\pi h/24)
\]

\[
Hour\_Cos = \cos(2\pi h/24)
\]

This representation preserves the circular nature of time, ensuring that times close to midnight remain close in the feature space.

### 3. Clustering Algorithms

**K-Means**
- Tested K values from 2 to 10.
- Used the Elbow Method and Silhouette Score.
- Selected K = 4 based on the elbow method and interpretability.

**DBSCAN**
- Used a 10-nearest-neighbour distance graph to investigate epsilon.
- Tested epsilon values from 0.0002 to 0.0005.
- Selected epsilon = 0.0005 with min_samples = 10.

**Agglomerative Clustering**
- Used Ward linkage.
- Applied clustering to a random sample of 3,000 bookings due to computational constraints.
- Selected four clusters.
- Visualized the hierarchy using a dendrogram.

## Results

| Algorithm | Clusters | Silhouette Score | Observations |
|---|---:|---:|---|
| K-Means | 4 | 0.5123 | Four temporal groups |
| DBSCAN | 301 | Not calculated | 6,328 noise points (4.22%) |
| Agglomerative | 4 | 0.4876 | Applied to 3,000 samples |

### Key Findings

- Booking activity is particularly low between midnight and 4 AM.
- Booking demand increases during the morning.
- A strong increase occurs during the afternoon and evening.
- 6 PM records the highest booking volume.
- K-Means produces four interpretable temporal groups.
- DBSCAN produces a large number of fragmented clusters for this feature representation.
- Agglomerative Clustering identifies four groups on the sampled dataset.

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- SciPy
- Jupyter Notebook

## Repository Structure

```text
uber-ride-booking-clustering/
│
├── Dataset/
│   └── ncr_ride_bookings.csv
│
├── dataset_cleaning.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/Riddhimaan22/uber-ride-booking-clustering.git
```

2. Navigate into the project directory:

```bash
cd uber-ride-booking-clustering
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Launch Jupyter Notebook:

```bash
jupyter notebook
```

5. Open `dataset_cleaning.ipynb` and run the cells sequentially.

Ensure the dataset is available at `Dataset/ncr_ride_bookings.csv`.

## Limitations

- Agglomerative Clustering was performed on a sample of 3,000 records rather than the entire dataset.
- DBSCAN produced many small clusters with the selected density parameters.
- The clustering analysis focuses on temporal features and does not incorporate geographical or ride-related characteristics.
- The K-Means and Agglomerative silhouette scores were initially calculated on different sets of observations.

## Dataset Attribution and License

This project uses the [Uber Ride Analytics Dashboard](https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard) dataset created and published by **Yash Dev Laddha** on Kaggle.

- **Source:** [Kaggle – Uber Ride Analytics Dashboard](https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard)
- **Author:** Yash Dev Laddha
- **Usage in This Project:** Used strictly for academic/educational analysis to perform time-of-day clustering (K-Means, DBSCAN, and Hierarchical Clustering) on ride booking timestamps and hourly trip patterns.
- **Note:** Raw dataset files are not redistributed in this repository; please download the CSV directly from the Kaggle link above to run the notebooks/scripts.

The dataset is distributed under the Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) license.

Original dataset source and creator: **[Insert original dataset source and creator attribution]**

Dataset license: https://creativecommons.org/licenses/by-sa/4.0/

Any redistribution or adaptation of the dataset must comply with the license terms, including attribution and ShareAlike requirements.

## Author

**Riddhimaan S Mahesh**

B.Tech Computer Science and Engineering  
Indian Institute of Information Technology, Guwahati

GitHub: https://github.com/Riddhimaan22

---

This project was developed as part of a university Machine Learning project.
