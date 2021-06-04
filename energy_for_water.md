---
layout: index
title: Energy for Water
prev: supply_water.html
next: outputs_quantity.html
gcam-version: v5.3 
---

# Table of Contents

- [Inputs to the Model](#inputs-to-the-model)
- [Description](#description)
- [Equations](#equations)
- [Insights and intuition](#insights-and-intuition)
- [References](#references)

## Inputs to the Model
**Table 1: Input data required for energy-for-water (EFW)**

| Name | Resolution | Unit | Source |
| :--- | :--- | :--- | :--- |
| Energy intensities of EFW processes (desalination, abstraction, treatment, distribution, wastewater treatment) | Global | GJ per $$m^3$$ | [Liu et al. 2016](energy_for_water.html#liu2016) |
| Irrigation water withdrawals | By region, GLU, crop | $$km^3$$ per year | [GCAM water demand](demand_water.html) |
| Municipal water withdrawals | By nation | $$km^3$$ per year | [GCAM water demand](demand_water.html) |
| Industrial water withdrawals | By nation | $$km^3$$ per year | [GCAM water demand](demand_water.html) |
| Desalinated water production | By nation | $$km^3$$ per year | FAO Aquastat |
| Shares of wastewater treated | By nation | Unitless | [Liu et al. 2016](energy_for_water.html#liu2016) |
| Non-renewable groundwater supply curves - electricity inputs | 20 grades per geopolitical region and GLU | GJ per $$m^3$$ | <a href="https://github.com/JGCRI/superwell">Superwell</a> |


## Description

### System boundaries
The specific system boundaries are explained in [Kyle et al. (2016)](energy_for_water.html#kyle2016), and are set so as to include all energy for activities whose primary output is water, and to exclude from this domain production technologies that use both energy and water as inputs to produce some other good. For example, in thermoelectric power generation, energy is applied to water, and several studies of energy-for-water (e.g., [Sanders and Webber 2012](energy_for_water.html#sanders2012)) have included it. This is not represented in GCAM as an "energy-for-water" process; rather, GCAM's representation of thermoelectric power generation consists of technologies that consume inputs of energy and water, and produce electricity as an output. The system boundaries of "energy-for-water" (EFW) consist of the following activities:

* Water abstraction
* Water treatment
* Water distribution
* Wastewater treatment

Within the following sectors:

* Desalinated water supply
* Irrigated crop production
* Industrial manufacturing
* Municipal water supply

### Modeling Energy-for-Water
The modeling approach is documented in [Kyle et al. (2021)](energy_for_water.html#kyle2021), and consists of the following steps:

* Estimation of water flow volumes of EFW processes and sectors
* Multiplication of water flow volumes by assumed energy intensities
* Adjustment of historical energy consumption in the commercial and industrial sectors to accommodate explicitly represented EFW

#### Water Flow Volumes
As indicated in Table 1, the historical water flow volumes for several of the sectors and processes are estimated in the [GCAM water demand](demand_water.html) part of the model, but even still several modifications are made. Table 2 shows the specific methods of estimation of each modeled water sector and process in the model, as well as the sectors from which base-year energy is re-allocated, and how the demands for each of these water flow volumes are driven in the future time periods.

**Table 2: Methods of estimation of water flow volumes by EFW sectors and processes**

| Sector | Process | Historical data source | Energy deducted from | Future demand driver |
| :--- | :--- | :--- | :--- | :--- |
| Desalinated water | Treatment | FAO Aquastat | Industry Sector; Commercial and Public Services | Municipal water demand; manufacturing water demand |
| Irrigation water | Abstraction | [Irrigation water withdrawals](demand_water.html), plus upstream distribution losses <sup>[1](#table2_footnote1)</sup> | Agriculture; Commercial and Public Services | Irrigation water demand |
| Industry | Abstraction | [Industrial water withdrawals](demand_water.html), minus desalinated water use <sup>[2](#table2_footnote2)</sup> | Industry Sector | Industrial Output |
| Industry | Treatment | [Industrial water withdrawals](demand_water.html), minus desalinated water use <sup>[2](#table2_footnote2)</sup> | Industry Sector | Industrial Output |
| Industry | Wastewater Treatment | [Industrial water withdrawals](demand_water.html), times wastewater treatment share <sup>[3](#table2_footnote3)</sup> | Industry Sector | Industrial Output |
| Municipal | Abstraction | [Municipal water withdrawals](demand_water.html), minus desalinated water use <sup>[2](#table2_footnote2)</sup> | Commercial and Public Services | Municipal water demand |
| Municipal | Treatment | [Municipal water withdrawals](demand_water.html), minus desalinated water use <sup>[2](#table2_footnote2)</sup> | Commercial and Public Services | Municipal water demand |
| Municipal | Distribution | [Municipal water withdrawals](demand_water.html) | Commercial and Public Services | Municipal water demand |
| Municipal | Wastewater Treatment | [Municipal water withdrawals](demand_water.html), times wastewater treatment share <sup>[3](#table2_footnote3)</sup> | Commercial and Public Services | Municipal water demand |

<a name="table2_footnote1">1</a>: Upstream conveyance losses are from the nation-level estimates of [Rohwer et al. 2007](energy_for_water.html#rohwer2007).

<a name="table2_footnote2">2</a>: Historical desalinated water production is assigned to municipal and industrial consumers on the basis of the relative shares of each sector's water withdrawal volumes

<a name="table2_footnote3">3</a>: Historical shares of wastewater treatment are estimated as the respective sector's withdrawal volume, minus consumptive uses, times the region's wastewater treatment shares, estimated by nation in [Liu et al. 2016](energy_for_water.html#liu2016). In the future these shares increase with per-capita GDP, similar to the representation of pollutant emissions abatement in the [Emissions module](emissions.html).

#### Energy Intensities
With the exception of water abstraction, the energy intensities by sector and process used in GCAM are equal across all regions, and are equal to the 50th percentile of the energy intensities, first published in [Liu et al. 2016](energy_for_water.html#liu2016) and later re-published with slight modifications in Table S3 of [Kyle et al. (2021)](energy_for_water.html#kyle2021). The inter-regional variation in abstraction-related energy intensity comes from region- and sector-specific shares of groundwater versus surface water. The values are shown in Table 3.

**Table 3: Assumed Energy Intensities by process**

| Sector | Process | Fuel | Energy Intensity <br> (kWh per $$m^3$$) |
| :--- | :--- | :--- | :-: |
| Desalinated water | Reverse osmosis | Electricity | 2.75 |
| Desalinated water | Thermal distillation | Natural gas or liquid fuels | 58.3 |
| Irrigation water | Abstraction - surface water | Electricity | 0.079 |
| Irrigation water | Abstraction - ground water | Electricity | 0.185 |
| Industry | Abstraction - surface water | Electricity | 0.079 |
| Industry | Abstraction - ground water | Electricity | 0.185 |
| Industry | Treatment | Electricity | 0.178 |
| Industry | Wastewater Treatment | Electricity | 0.775 |
| Municipal | Abstraction - surface water | Electricity | 0.079 |
| Municipal | Abstraction - ground water | Electricity | 0.185 |
| Municipal | Treatment | Electricity | 0.235 |
| Municipal | Distribution | Electricity | 0.247 |
| Municipal | Wastewater Treatment | Electricity | 0.597 |

Electricity used for non-renewable groundwater pumping is represented in future periods, using exogenous supply curves that have been constructed from simulated groundwater pumping over an 80 year period in <a href="https://github.com/JGCRI/superwell">Superwell</a>. The methods used are documented in [Turner et al. 2019](energy_for_water.html#turner2019) and [Kyle et al. (2021)](energy_for_water.html#kyle2021). From the Superwell output, supply curves are constructed for each GCAM region and water basin that consist of 20 "graded" points, each of which is assigned a total quantity of water, a non-energy-related cost of well construction and operation, and an electricity input-output coefficient. The grades are binned according to estimated total cost, using exogenous electricity prices; due to changes in electricity prices over time, the relative total costs of these grades may change over time.

## Equations 
The primary equation used in estimating energy-for-water by sector and process is as follows:

$$
EFW_{s,p}=W_{s,p}*EI_{s,p}
$$

Where $$EFW$$ is energy-for-water, $$s$$ is sector, $$p$$ is process, $$W$$ is water flow volume, and $$EI$$ is energy intensity. The energy intensity values for each process and sector were shown in the table above, and the water flow volumes are generally determined in [GCAM water demand](demand_water.html).

Non-renewable groundwater pumping energy intensity is estimated in Superwell for any well *i* according to the following equations, reproduced from [superwell.R](https://github.com/JGCRI/superwell/blob/master/R/superwell.R):

$$
Power_{i}=\frac{SpecificWeight*TotalHead_{i}*WellYield_{i}}{PumpEfficiency*WattsPerKW}
$$

$$
ElectricEnergyPerYear_{i}=Power_{i}*\frac{AnnualOperationTime}{SecondsPerHour}
$$

$$
ElectricEnergyIntensity_{i}=\frac{ElectricEnergyPerYear_{i}}{WellYield_{i}*AnnualOperationTime}
$$

Where $$Power$$ is in $$kW$$, $$SpecificWeight$$ is in $$kg/m^2/s^2$$, $$WellYield$$ is in $$m^3/s$$, PumpEfficiency is unitless, assumed to be 50%, and $$WattsPerKW$$ is a constant, equal to 1000.

$$ElectricEnergyPerYear$$ is in $$kWh/yr$$, $$AnnualOperationTime$$ is in seconds per year, and $$SecondsPerHour$$ is a constant, equal to 3600.

$$ElectricEnergyIntensity$$ is in $$kWh/m^3$$.


## Insights and intuition

### Modeling Energy-for-water in GCAM

[Kyle et al. (2021)](energy_for_water.html#kyle2021) demonstrate a surprisingly small net impact on future global energy use from disaggregating energy-for-water in GCAM, as the water-related demands of electricity often parallel the future projected energy growth in the commercial and industrial sectors from which EFW energy is re-allocated. For example, energy for industrial water abstraction, treatment, and post-use wastewater treatment scale with the sector's water demands, which are driven by the sector's output, which is also what drives its demands for energy in the first place. So, representing energy-for-water explicitly in the model does not necessarily cause a departure in projected future energy demands, depending on the sector and region. The study also demonstrates that efforts to improve water provision and quality, as specified in Sustainable Development Goal #6, build off of one another in terms of energy-for-water. Expanding municipal water access to all people will increase the volume of wastewater generated, and parallel efforts to treat the maximum possible portion of wastewater will further increase the energy required for wastewater treatment, to levels that are multiples above a "business-as-usual" scenario.


## References

<a name="kyle2016">[Kyle et al. 2016]</a> Kyle, P., Johnson, N., Davies, E., Bijl, D.L., Mouratiadou, I., Bevione, M., Drouet, L., Fujimori, S., Liu, Y., and Hejazi, M. 2016. Setting the system boundaries of “energy for water” for integrated modeling. *Environmental Science & Technology 50(17), 8930-8931. [Link](https://pubs.acs.org/doi/abs/10.1021/acs.est.6b01066)

<a name="kyle2021">[Kyle et al. 2021]</a> Kyle, P., Hejazi, M., Kim, S., Patel, P., Graham, N., and Liu, Y. 2021. Assessing the future of global energy-for-water. *Environmental Research Letters* 16(2), 024031. [Link](https://iopscience.iop.org/article/10.1088/1748-9326/abd8a9)

<a name="liu2016">[Liu et al. 2016]</a> Liu, Y., Hejazi, M., Kyle, P., Kim, S., Davies, E., Miralles, D., Teuling, A., He, Y., and Niyogi, D. 2016. Global and Regional Evaluation of Energy for Water. *Environmental Science & Technology* 50(17), 9736-9745. [Link](https://pubs.acs.org/doi/abs/10.1021/acs.est.6b01065)

<a name="rohwer2007">[Rohwer et al. 2007]</a> Rohwer, J., Gerten, D., and Lucht, W. 2007. *Development of Functional Irrigation Types for Improved Global Crop Modelling*. PIK Report No. 104, Potsdam Institute for Climate Impact Research. [Link](https://www.pik30 potsdam.de/research/publications/pikreports/.files/pr104.pdf)

<a name="sanders2012">[Sanders and Webber 2012]</a> Sanders, K., and Webber, M. 2012. Evaluating the energy consumed for water use in the United States. *Environmental Research Letters* 7(3), 0034034. [Link](https://iopscience.iop.org/article/10.1088/1748-9326/7/3/034034/meta)

<a name="turner2019">[Turner et al. 2019]</a> Turner, S.W.D., Hejazi, M., Yonkofski, C., Kim, S.H., and Kyle, P. 2019. Influence of groundwater extraction costs and resource depletion limits on simulated global nonrenewable water withdrawals over the twenty-first century. *Earth’s Future* 7, 123-135. [Link](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2018EF001105)
