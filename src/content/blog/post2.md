---
title: "Building the Ensemble model: My approach"
description: "This blog outlines my process of building an ensemble model to predict F10.7 to automate ground support stations.I take a deep dive into the Exploratory Data Analysis and the individual models that consitute the ensemble model."
pubDate: "Sep 11 2022"
heroImage: "/solar.webp"
---

**Problem Statement:**

The F10.7 index, a measure of solar radio flux at a wavelength of 10.7 cm, is a crucial parameter for understanding solar activity. It significantly impacts atmospheric drag, which in turn affects satellite speed and orbit decay. Accurate prediction of the F10.7 value is vital for automating ground support stations, optimizing satellite operations, and ensuring mission success. The challenge was to build a predictive model for F10.7 that leverages historical data and advanced modeling techniques.

**Data Collection and Preparation:**

To build the model, I retrieved historical F10.7 data dating back to 1950 using HTTP GET requests from CelesTrak. The data was meticulously cleaned and formatted to create a robust dataset. However, I started the analysis from 1954 because that marked the beginning of a new solar cycle, providing a more consistent basis for modeling.

An extensive Exploratory Data Analysis (EDA) was conducted on this dataset to uncover any hidden patterns, such as weekly, monthly, or yearly trends. Understanding these patterns was essential to refine the modeling approach and ensure that no significant cyclical behavior was overlooked.

The solar cycle typically runs in an 11-year pattern, with values generally increasing from the start of the cycle to the midpoint (solar maximum) and then decreasing towards the end (solar minimum). This cyclical nature of solar activity was a key consideration in the modeling process.

**The Ensemble Approach:**

Given the cyclical and complex nature of the solar cycle, a single model might not capture all the nuances of the data. Therefore, I employed an ensemble approach, combining three distinct models:

LSTM (Long Short-Term Memory): LSTM is a type of recurrent neural network (RNN) that is well-suited for time series forecasting, especially when long-term dependencies are present. Given that the solar cycle spans 11 years, LSTM's ability to retain information over long sequences made it an ideal candidate for capturing the cyclic patterns in the F10.7 index. I assigned the maximum weight to the LSTM model because it could effectively model the temporal dependencies and nonlinearities in the data.

Facebook Prophet: Prophet is a model specifically designed for forecasting time series data that exhibits strong seasonal patterns and holiday effects. The solar cycle's predictable 11-year pattern aligns well with Prophet's capabilities, making it a valuable component of the ensemble.

Gradient Regressor: To account for any linear trends and potential external factors influencing F10.7, I included a Gradient Regressor in the ensemble. This model helps to capture any residual patterns that might not be well-represented by the LSTM and Prophet models.

The ensemble model, with a weighted combination of these three approaches, was designed to balance the strengths of each individual model, ensuring that the predictions are both accurate and robust. When measured against historical data, the ensemble achieved a prediction accuracy of 85%, demonstrating its effectiveness in forecasting F10.7.

**Understanding Atmospheric Drag:**

This project wasn't just about building a predictive model; it also involved extensive research into atmospheric drag and its implications for satellite operations. Atmospheric drag is influenced by various factors, including solar activity, and it plays a critical role in determining satellite orbits and lifespans. By predicting F10.7, ground support stations can better anticipate changes in atmospheric drag, allowing for more precise satellite tracking and orbit adjustments.

**Conclusion:**

The ensemble model I developed, combining LSTM, Facebook Prophet, and Gradient Regressor, provides a powerful tool for predicting F10.7. With this model, we can automate ground support stations, enhance satellite mission planning, and ultimately contribute to more reliable and efficient space operations. The use of multiple models allows for a comprehensive approach that captures the complex dynamics of the solar cycle, ensuring that our predictions are as accurate as possible.