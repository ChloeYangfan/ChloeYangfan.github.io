---
title: "Li et al. (2026) — Growing Impacts of Fire Smoke on Ozone Pollution and Associated Mortality Burden in the United States"
parent: Literature
nav_order: 2
---

# Li et al. (2026) — Growing Impacts of Fire Smoke on Ozone Pollution and Associated Mortality Burden in the United States

**Paper:** Li, Y., Jin, X., Kelp, M., Sun, H. Z., & Qiu, M. (2026). *Growing impacts of fire smoke on ozone pollution and associated mortality burden in the United States*. Science Advances, 12, eaec2903.  
**Topic:** wildfire smoke, ozone, PM2.5, health burden, mortality, machine learning, air quality  
**My keywords:** smoke O3, smoke PM2.5, fire emissions, ozone precursor chemistry, wildfire health impact, long-range smoke transport, pyroCb relevance

---

## 1. Research Question and Overall Design

The central question of this paper is: **How much does fire smoke contribute to ground-level ozone (O3) pollution and the associated mortality burden in the United States?**

Most wildfire-smoke health studies focus on fine particulate matter (PM2.5). This paper argues that this focus is incomplete because fire smoke also emits ozone precursors, especially VOCs and NOx, which can enhance ground-level O3 through photochemical reactions. O3 is itself a regulated air pollutant and has well-established health impacts.

The authors ask several related questions:

1. Does ground-level O3 increase on smoke days relative to comparable nonsmoke days?
2. Are smoke O3 patterns similar to or different from smoke PM2.5 patterns?
3. How much do smoke-related O3 increases contribute to O3 exceedance days?
4. How large is the mortality burden from smoke O3 compared with total O3 and smoke PM2.5?
5. Has the importance of smoke O3 changed from 2006 to 2023?

The overall design is observational and counterfactual. The authors identify smoke days using NOAA HMS smoke plume polygons and compare observed daily maximum 8-hour average O3 (MDA8 O3) on those smoke days with a baseline O3 level estimated from meteorologically similar nonsmoke days at the same monitoring site. The difference is defined as **smoke O3**:

\[
\text{Smoke } O_3 = O_{3,\text{observed on smoke day}} - O_{3,\text{baseline on similar nonsmoke days}}
\]

They then compare smoke O3 with smoke PM2.5, analyze O3 exceedance events, use machine-learning models as an alternative counterfactual approach, and estimate mortality burden using existing exposure-response functions.

---

## 2. Data Products, Variables, Time Range, and Spatial Range

### Time Range

The study covers **2006–2023**. For the health impact analysis, the authors focus on the **warm season**, defined as **April to September**, following the epidemiological literature on O3 exposure.

### Spatial Range

The spatial domain is the **contiguous United States (CONUS)**. Many analyses distinguish between the western and eastern United States, using **100°W** as the dividing line.

### Main Data Products

#### Surface O3

The authors use hourly O3 measurements from the **US EPA AirData** repository. They calculate daily **MDA8 O3**, or maximum daily 8-hour average O3. The analysis includes **1835 O3 monitoring sites** that operated at some point during 2006–2023.

#### Surface PM2.5 and Smoke PM2.5

Daily PM2.5 measurements also come from EPA AirData. In addition, the authors use gridded daily **smoke PM2.5 estimates** from Childs et al., available at 10-km resolution over the contiguous US. These smoke PM2.5 data are used to compare smoke O3 and smoke PM2.5 patterns and to test more stringent definitions of smoke days.

#### Smoke Plumes

Smoke days are primarily identified using the **NOAA Hazard Mapping System (HMS)** smoke plume product. A monitoring site is classified as having a smoke day if it intersects with an HMS smoke plume polygon on that day.

#### Fire Activity

The authors use **MODIS Active Fire** products, including fire locations and fire radiative power (FRP). These data are used to examine how smoke O3 varies with distance from active fires and fire intensity.

#### Ozone Precursors

The authors use surface **NO2** and **HCHO** from ECMWF Atmospheric Composition Reanalysis 4 (EAC4) as indicators of ozone precursor availability. NO2 is related to NOx chemistry, while HCHO is often used as a proxy for VOC oxidation.

#### Meteorology

The main meteorological controls are:

- surface temperature from gridMET,
- UV radiation from ERA5,
- and additional ERA5 / ERA5-Land variables for the machine-learning model, including temperature, dewpoint, pressure, wind, precipitation, cloud cover, boundary layer height, soil moisture, and leaf area index.

#### Population and Mortality

Population data come from the US Census Bureau’s Gridded Environmental Impacts Frame. Mortality calculations are based on county-level population, baseline mortality rates, and established exposure-response functions for O3 and smoke PM2.5.

### Key Variables

The most important variables are:

- **MDA8 O3:** maximum daily 8-hour average ozone.
- **Smoke O3:** observed O3 on smoke days minus meteorologically matched nonsmoke baseline O3.
- **Smoke PM2.5:** estimated smoke-attributable PM2.5.
- **O3 exceedance:** days when MDA8 O3 exceeds 70 ppb.
- **Smoke-driven O3 exceedance:** days when baseline nonsmoke O3 is below 70 ppb, but total O3 exceeds 70 ppb because of smoke O3.
- **Excess deaths due to smoke O3:** mortality attributable to smoke-related O3 exposure.

---

## 3. Core Logic of the Method

The core methodological challenge is that smoke days are often meteorologically different from nonsmoke days. Smoke days may be hotter and sunnier, and both high temperature and strong UV radiation favor O3 formation. Therefore, a simple smoke-day versus nonsmoke-day comparison would overestimate the smoke effect.

To address this, the authors construct a meteorologically matched nonsmoke baseline.

For each smoke day at each monitor, they identify nonsmoke days that satisfy the following conditions:

1. same monitoring site,
2. same season,
3. within a 3-year window centered on the smoke year,
4. ambient temperature within 1°C of the smoke day,
5. UV radiation within \(10^4\ \mathrm{J\ m^{-2}}\) of the smoke day.

The mean MDA8 O3 across those matched nonsmoke days is treated as the counterfactual O3 concentration that would have occurred without smoke. The difference between observed smoke-day O3 and this matched baseline is interpreted as smoke O3.

The authors also build machine-learning counterfactual models. They train XGBoost, CatBoost, and neural network models on nonsmoke days only, then use an ensemble model to predict counterfactual O3 on smoke days under the same meteorological conditions. This provides an alternative way to estimate how much O3 would have occurred without smoke.

For mortality, the authors spatially interpolate smoke O3 to a 10-km grid, aggregate exposure to the county level, and apply published exposure-response functions. Importantly, the O3 exposure-response function is based on all-source O3, not smoke-specific O3, which is an important limitation.

---

## 4. Robustness Checks and Uncertainty Analysis

### Smoke Day Definition

The main smoke-day definition uses HMS smoke plumes. However, HMS plumes may include smoke aloft that does not affect surface air quality. To test this uncertainty, the authors apply more stringent smoke-day definitions by requiring HMS smoke days to also show evidence of increased surface PM2.5 or estimated smoke PM2.5.

The main conclusions remain robust: smoke O3 has a different spatial-temporal pattern from smoke PM2.5, and smoke O3 mortality becomes increasingly important in recent years.

### Meteorological Adjustment

The authors compare several methods:

- no meteorological control,
- temperature-only matching,
- UV-only matching,
- temperature-and-UV matching,
- machine-learning counterfactual estimates.

They find that temperature and UV explain about half of the apparent O3 enhancement on smoke days. The observation-based method estimates that meteorology explains roughly 50% of the enhancement, while the ML method estimates about 58%. The ML method generally gives lower smoke O3 estimates, but the qualitative conclusions remain similar.

### PM2.5 Threshold Sensitivity

The authors show that smoke days with very low smoke PM2.5 contribute little to smoke O3 mortality. This suggests that potential misclassification of weak smoke days by HMS does not dominate the mortality estimates.

### Health Function Uncertainty

A major uncertainty is that there is no established long-term exposure-response function specifically for smoke O3. The authors use an all-source O3 exposure-response function. This could bias the health burden estimate because smoke O3 occurs with co-emitted pollutants such as PM2.5, VOCs, NOx, and organic aerosol, and because smoke exposure is more episodic than typical urban O3 exposure.

### Spatial Exposure Uncertainty

The mortality analysis requires interpolating monitor-level O3 to gridded and county-level exposure. This may miss fine-scale spatial gradients, especially in rural or mountainous regions with sparse monitors. The authors expect this uncertainty to be less severe for warm-season average exposure than for daily local exposure.

---

## 5. Main Results

First, O3 is often higher on smoke days. Across the US, MDA8 O3 is higher on 62% of smoke days compared with meteorologically matched nonsmoke days. At some monitoring locations, average smoke O3 reaches 6.9 ppb, corresponding to a 16% increase relative to nonsmoke baseline O3.

Second, smoke O3 and smoke PM2.5 have different spatial patterns. Smoke PM2.5 tends to be highest in the western US, where fire activity is intense and smoke concentrations are often large. In contrast, smoke O3 enhancement is often larger in the eastern and southeastern US. This means that PM2.5 is not a reliable proxy for smoke O3.

Third, the relationship between smoke PM2.5 and smoke O3 is nonlinear. At low smoke PM2.5 levels, smoke O3 and smoke PM2.5 are weakly positively correlated. At high smoke PM2.5 levels, this relationship weakens or reverses, likely because dense smoke aerosol can reduce photolysis rates and suppress O3 production.

Fourth, smoke-driven O3 exceedances are becoming more important. Overall O3 exceedance days have declined over time, mainly because nonsmoke O3 has declined. However, smoke-driven exceedances have not declined in the same way. In some recent extreme smoke years, smoke accounts for a large fraction of O3 exceedances.

Fifth, smoke O3 causes a substantial and growing mortality burden. The authors estimate an average of **2045 annual excess deaths** from smoke O3 among the elderly population during 2006–2023. Smoke O3 mortality equals about **15.8% of smoke PM2.5 mortality** over the full study period, and this ratio reaches **61.5% in 2023**.

The key takeaway is that wildfire smoke health risk cannot be fully characterized by PM2.5 alone. O3 is an increasingly important part of smoke-related air pollution and health burden.

---

## 6. Main Message of Each Figure

### Figure 1: Surface O3 Increases on Smoke Days

Figure 1 compares O3 on smoke days, baseline O3 on meteorologically similar nonsmoke days, smoke O3, and relative O3 change.

Panel A shows MDA8 O3 on smoke days. High total O3 appears in many western and southwestern locations.

Panel B shows the estimated nonsmoke baseline O3 under similar meteorology.

Panel C shows smoke O3, defined as the difference between smoke-day O3 and baseline O3. The largest smoke O3 enhancements are not necessarily in the same places as the highest total O3.

Panel D shows relative O3 enhancement. The southeastern US shows strong relative increases.

My takeaway from Figure 1 is that smoke O3 is spatially distinct from both total O3 and smoke PM2.5. The eastern US, especially the Southeast, appears particularly sensitive to smoke-related O3 enhancement.

### Figure 2: Annual Average Smoke O3 from 2006 to 2023

Figure 2 maps annual average smoke O3 for each year from 2006 to 2023. Smoke O3 shows strong interannual variability. The largest years include 2023, 2021, 2022, and 2012.

The 2023 map is especially striking because high smoke O3 extends across a large region from the Midwest to the southeastern US. This reflects the influence of extreme smoke transport events, including long-range transport from major fires.

My takeaway from Figure 2 is that smoke O3 is not just a local fire problem. It can become a regional to continental-scale air quality issue.

### Figure 3: Smoke Contributions to O3 Exceedance Days

Figure 3 separates O3 exceedance days into smoke-driven and not smoke-driven categories.

A smoke-driven exceedance occurs when the nonsmoke baseline O3 is below 70 ppb, but total O3 exceeds 70 ppb because of smoke O3.

Both the western and eastern US show declining total O3 exceedance frequency over time, but much of this decline comes from nonsmoke exceedances. Smoke-driven exceedances remain important and can dominate in some recent years.

My takeaway from Figure 3 is that wildfire smoke can offset some of the air-quality gains achieved by reducing anthropogenic O3 precursors.

### Figure 4: Nonlinear Relationship Between Smoke PM2.5 and Smoke O3

Figure 4 bins observations by daily smoke PM2.5 and compares the distribution of smoke O3 in the eastern and western US.

At low smoke PM2.5, smoke O3 tends to increase with smoke PM2.5. At higher smoke PM2.5, the relationship weakens and can reverse. The eastern US often has higher smoke O3 than the western US within the same smoke PM2.5 bin.

My takeaway from Figure 4 is that smoke PM2.5 cannot be used as a simple proxy for smoke O3. O3 formation depends on nonlinear chemistry, photolysis, precursor availability, and meteorology, not only on smoke mass.

### Figure 5: Driving Factors of Smoke O3

Figure 5 examines why smoke O3 changes.

Panel A compares smoke O3 estimates under different meteorological correction methods. Without meteorological correction, smoke-day O3 enhancement is large. After controlling for temperature and UV, the enhancement is reduced by about half.

Panel B shows contributions from different conditions related to precursors, distance from fires, and FRP. A large fraction of smoke O3 burden occurs when NO2 and/or HCHO are elevated. The results also show that smoke O3 can occur far from fires, not only near active burning.

My takeaway from Figure 5 is that smoke O3 is controlled by a combination of meteorology, precursor chemistry, transport distance, and fire intensity.

### Figure 6: Mortality Burden from Smoke O3

Figure 6 estimates excess deaths due to smoke O3 and compares them with nonsmoke O3 and smoke PM2.5 mortality.

Panel A shows that nonsmoke O3 mortality has declined, while smoke O3 mortality has increased.

Panel B shows state-level smoke O3 death rates, with high burdens in parts of the southern and eastern US.

Panel C compares smoke O3 deaths and smoke PM2.5 deaths across states. Some states experience high burdens from both, while others have high PM2.5 burden but relatively lower O3 burden.

Panel D shows that smoke O3 mortality mainly comes from moderate smoke PM2.5 days rather than the most extreme PM2.5 days.

Panel E compares annual deaths from smoke O3 and smoke PM2.5. In 2023, smoke O3 mortality becomes comparable in magnitude to smoke PM2.5 mortality.

My takeaway from Figure 6 is that smoke O3 is a growing health risk that is spatially and temporally different from smoke PM2.5.

---

## 7. Limitations, Future Directions, and Connections to My Research

### Limitations

The first limitation is smoke-day identification. HMS smoke plumes are based on satellite interpretation and do not necessarily indicate surface smoke exposure. Some smoke may be aloft, while some surface smoke may be missed. The authors address this with PM2.5-based sensitivity tests, but more physically based smoke attribution would be valuable.

The second limitation is the separation between smoke effects and meteorological effects. The authors treat temperature and UV as confounders, but intense smoke can itself modify radiation, boundary-layer structure, and possibly temperature. Therefore, removing meteorological variability may also remove part of the smoke-induced atmospheric response.

The third limitation is that the study does not fully resolve O3 chemistry mechanisms. NO2 and HCHO are useful precursor indicators, but the analysis does not explicitly separate VOC-limited and NOx-limited chemical regimes, PAN transport, plume aging, aerosol effects on photolysis, or heterogeneous chemistry.

The fourth limitation is the health impact function. The mortality calculation uses an all-source O3 exposure-response function, not a smoke-specific O3 function. Smoke O3 occurs as part of a complex pollution mixture, so the health effect may differ from that of background urban O3.

The fifth limitation is spatial exposure representation. EPA monitors are unevenly distributed and may not fully capture smoke O3 exposure in rural, mountainous, or fire-adjacent regions.

### Future Directions

This paper points to several future research directions.

First, chemical transport models such as WRF-Chem, GEOS-Chem, or CMAQ could be used to separate the contributions of fire emissions, meteorology, plume chemistry, and long-range transport to smoke O3.

Second, future epidemiological work should develop smoke-specific O3 exposure-response functions and examine joint health impacts from smoke PM2.5 and smoke O3.

Third, smoke warning systems should include O3, not only PM2.5. Moderate smoke events may still produce substantial O3 health burden even when PM2.5 is not extremely high.

Fourth, future work should better represent vertical smoke injection, plume aging, and the coupling between aerosol, radiation, clouds, and chemistry.

### Connections to My Research on PyroCb, ACI, and Wildfire

This paper is closely related to my research because it shows that wildfire smoke impacts are not limited to PM2.5. Smoke also affects O3, and the spatial pattern of smoke O3 can differ strongly from smoke PM2.5. This is important for pyroCb research because pyroCbs strongly modify the vertical distribution of smoke.

My work focuses on how biomass-burning aerosols and aerosol-cloud interactions influence pyroCb dynamics and upper-tropospheric smoke transport. If aerosol-cloud interactions enhance sustained vertical transport, they may change where smoke, CO, aerosols, and O3 precursors are injected, transported, and eventually mixed back toward the surface. This could affect downwind O3 production and exposure patterns.

This paper also helps me frame the broader significance of pyroCb smoke injection. PyroCbs are often discussed in terms of UTLS smoke, radiative effects, and long-range transport. However, this paper suggests another important angle: changes in smoke transport pathways may also influence surface air quality and health through O3 chemistry, not only through PM2.5.

For my own manuscript, this paper could be useful in the introduction or broader-impact discussion. I can use it to argue that accurately simulating wildfire smoke transport, especially deep injection by pyroCbs, matters for understanding not only climate-relevant smoke lifetime and UTLS aerosol loading, but also downwind air quality and human health impacts.

---

## 8. Summary in One Paragraph

Li et al. (2026) quantify how fire smoke affects ground-level ozone and related mortality across the contiguous United States from 2006 to 2023. Using EPA surface O3 observations, NOAA HMS smoke plumes, meteorological data, satellite/reanalysis products, and machine-learning counterfactual models, they define smoke O3 as the difference between observed MDA8 O3 on smoke days and meteorologically matched nonsmoke baseline O3. They find that smoke increases O3 at many monitors, with enhancements up to 6.9 ppb and relative increases up to 16% after correcting for temperature and UV variability. Smoke O3 patterns differ strongly from smoke PM2.5: enhancements are often larger in the eastern and southeastern US, and the O3-PM2.5 relationship weakens or reverses under very high smoke PM2.5. Smoke-driven O3 exceedances have become increasingly important as nonsmoke O3 exceedances decline. Using established all-source O3 exposure-response functions, the authors estimate 2045 annual excess deaths from smoke O3 among the elderly, averaged over 2006–2023; by 2023, smoke O3 mortality approached the magnitude of smoke PM2.5 mortality. The study highlights that wildfire smoke health risks cannot be characterized by PM2.5 alone and that future smoke risk assessment should include O3 chemistry, long-range transport, and smoke-specific health functions.
