# Private and Public Good Provision of Mental Health Services in France

An empirical data analysis project studying how private mental health services interact with public mental health provision in France.
Team : Salma El Aazdoudi, Cynthia Francis, Rafael Mourouvin and Anahi Reyes

## Overview

This project explores the relationship between **private therapists** and **public mental health centers (CMPs)** across French departments. Using data collected from **Psychologue.net** and combined with public datasets from **DREES** and **INSEE**, the analysis investigates whether the private sector substitutes for gaps in state-provided mental health services.

## Research Question

**To what extent is the private sector substituting for state-provided mental health services in France?**

## Main Findings

- Departments with a **higher density of CMPs** tend to have **fewer independent therapists**, suggesting a substitution effect.
- **Therapy prices vary geographically**, with pricing differences linked to distance and local service availability.
- **Online presence matters**: visibility, accessibility, and digital booking options are strongly related to therapist exposure and market reach.
- Some of the **least available private services** appear to overlap with areas traditionally covered by public mental health centers, suggesting possible complementarity in some cases.

## Data Sources

This project combines data from multiple sources:

- **Psychologue.net**
  - Therapist profiles
  - Appointment availability
  - Prices
  - Ratings
  - Services offered
  - Online consultation availability

- **DREES**
  - Data on **Centres Médico-Psychologiques (CMPs)** and public psychiatric care infrastructure

- **INSEE**
  - Geographic and demographic information
  - Density classifications and territorial indicators

## Data Collection

The therapist dataset was collected from a **hidden API** used by Psychologue.net, which allowed structured extraction without relying only on front-end scraping.

### Collected variables
- Therapist name
- Location
- Postal code
- Rating
- Number of ratings
- Price
- Available appointment slots
- Services offered
- Online availability

### Collection notes
- Data reflects therapists listed on the platform with open appointment slots
- Extraction dates: **December 23, 2024** and **January 13, 2025**
- Some professionals may not be represented if they are not listed on the platform or use offline booking methods

## Methodology

The project combines:

- **Web data collection**
- **Data cleaning and merging**
- **Descriptive statistics**
- **Geographic comparison**
- **Regression analysis**

The core empirical analysis estimates the relationship between:

- **Number of private/liberal therapists**
- **CMP density per capita**
- Geographic controls such as department area

## Results

The regression results show a **negative and statistically significant relationship** between CMP density and the number of liberal therapists across departments.

This supports the idea that where public mental health services are more available, the private sector may be less developed, indicating a potential **substitution effect**.

## Project Structure

```bash
.
├── data/
│   ├── raw/
│   ├── processed/
├── notebooks/
├── scripts/
├── outputs/
│   ├── figures/
│   ├── tables/
├── report/
├── README.md
