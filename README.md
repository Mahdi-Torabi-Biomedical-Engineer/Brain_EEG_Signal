# EEG Signal Processing with MATLAB: Alpha Source Separation and GED

## Overview

Electroencephalography (EEG) captures electrical activity from the brain using electrodes placed on the scalp. For this analysis, the focus is on isolating brain activity in the alpha frequency band (8-13 Hz), which is associated with various cognitive states such as relaxation, meditation, and attention. By applying Generalized Eigenvalue Decomposition (GED), we can extract spatial components that represent meaningful patterns in the alpha band, providing insights into brain connectivity and functional regions.

## Why Alpha Band?

The alpha band is a prominent rhythm in EEG that often reflects resting states or periods of relaxed wakefulness. The alpha band is typically stronger in the occipital and parietal regions when the brain is not actively engaged in specific tasks. Its significance in EEG studies lies in its association with processes like relaxation, attention, and sensory processing. The alpha rhythm is also often used to study brain disorders and cognitive impairments, where abnormal alpha activity can be indicative of dysfunction.

## Purpose of Source Separation in EEG

Brain activity is composed of signals from various overlapping sources, and separating these sources is crucial for understanding the underlying neural activity. By isolating specific frequency bands (like alpha) and applying source separation techniques, we can distinguish between different components of brain activity, which can be spatially or functionally distinct. This helps in pinpointing specific brain regions responsible for observed activity, improving signal interpretation and providing cleaner data for downstream analysis.

## Generalized Eigenvalue Decomposition (GED)

GED is a statistical technique that allows for optimal separation of source components based on desired features, such as specific frequency bands. In this context, GED is applied to separate alpha-band signals from other frequencies and identify unique sources. It operates by creating and comparing covariance matrices—statistical representations of signal variance—which capture the spatial structure of the signals in different conditions. GED finds the eigenvalues and eigenvectors that maximize the variance in the alpha-band signals relative to the broad spectrum EEG data, highlighting the strongest independent components.

## Step-by-Step Explanation

### 1. Load and Inspect Data

After loading the EEG dataset, the first step is to inspect its structure and visualize a sample of the time series data. This initial exploration helps ensure data integrity and provides a preliminary view of signal patterns across channels.
 

```matlab
load('restingstate.mat')

% Inspect the EEG data structure
EEG

% Plot a sample EEG signal
plot_simEEG(EEG,31,10)
```
![Figure 1: Example EEG Time Series](images/EEG_Time_Series.png)
### 2. Alpha Band Filtering

The alpha band is isolated by applying a bandpass filter to the EEG data. Filtering removes unwanted frequencies, which can interfere with the analysis of alpha-specific signals. By focusing only on the 8-13 Hz range, we capture the rhythmic activity characteristic of the alpha band, which is essential for analyzing resting state or attentional processes.


### 3. Covariance Matrices for Source Separation

Covariance matrices represent the variance structure of signals across channels, reflecting how signals change in tandem across the brain. For source separation, two matrices (S and R) are created:
- **S** represents the covariance of the alpha-filtered data, emphasizing variance patterns unique to the alpha band.
- **R** captures the covariance of the broader EEG signal, providing a baseline for comparison.

These matrices are averaged over trials to ensure robust estimation and are essential for the GED process, where we seek to maximize the separation of alpha-band activity from other signals.


![Figure 2: Covariance Matrices (S and R)](images/S_R.png)

### 4. Applying GED and Extracting Components

GED uses the covariance matrices to find eigenvalues and eigenvectors, which capture the strongest patterns of alpha-band activity. Sorting by eigenvalues enables us to identify components that represent the most prominent sources of variance in the data. These components are arranged in descending order of variance explained, allowing us to focus on the most significant patterns first.


![Figure 3: GED Eigenvalue Scree Plot](images/scree.png)


### 5. Component Time Series and Topographic Representation

Once the main components are identified, we compute their time series by projecting the EEG data onto these components. This projection creates new virtual channels that isolate each component's activity over time. Visualizing these topographies reveals the spatial origins of each component, indicating which regions of the brain contribute most to the observed alpha activity.


![Figure 4: Top Two GED Components](images/GED.png)

### 6. Phase Synchronization Analysis

Phase synchronization measures the degree to which oscillations in two signals are aligned over time. High synchronization in specific frequency bands suggests strong functional connectivity between brain regions. Here, we analyze the phase synchronization between the top two GED components across various frequencies, revealing how strongly different areas in the brain are linked in the alpha band and beyond.

The power spectrum represents the distribution of signal energy across different frequencies. By analyzing the power spectrum of the extracted components, we gain insight into the dominant frequencies within each component. For alpha-band studies, peaks in the power spectrum around 8-13 Hz would confirm the presence and strength of alpha activity.

![Figure 5: Phase Synchronization Spectrum](images/Phase.png)

### 7. Amplitude Correlation Across Components

Amplitude correlations between components show how the power of oscillations in different regions covaries over time. High correlations indicate that the amplitude changes in one region are mirrored by another, suggesting that these areas may be functionally connected or driven by the same underlying source. This analysis helps reveal patterns of synchronized activity across multiple brain regions, providing a broader picture of functional connectivity in the alpha band.


![Figure 6: Correlation Matrix for Amplitude Time Series](images/Correlation.png)



### 8. Topographic Mapping of Components

Finally, we visualize the spatial distribution of the strongest GED components using topographic maps. These maps illustrate the scalp locations most strongly associated with each component, highlighting brain regions where alpha-band activity is most prominent. This step is critical for understanding the spatial layout of functional brain networks associated with the alpha band.

![Figure 7: Correlation Matrix for Amplitude Time Series](images/8 components.png)

## Conclusion
This project showcases the potential of GED and alpha-band analysis for EEG signal processing, enabling in-depth exploration of brain connectivity and rhythmic activity. By isolating and analyzing alpha-band components, we can better understand the neural mechanisms underlying cognitive states and identify patterns of connectivity associated with various mental processes.




