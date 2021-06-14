---
layout: index
title: The GCAM Water Model
prev: supply_energy.html
next: supply_energy.html
gcam-version: v5.3 
---

This page provides more detailed explanations of the descriptions provided in the [Energy Supply](supply_energy.html) and [Energy Demand](demand_energy.html) modeling pages.

{:toc}

## Resources

### Depletable Resources 

The figures below show some illustrative examples of supply curves used within GCAM.

<img src="gcam-figs/oil_supply_curve.png" width="750" height="300" />
{: .fig}
<img src="gcam-figs/gas_supply_curve.png" width="750" height="300" />
{: .fig}
<img src="gcam-figs/coal_supply_curve.png" width="750" height="300" />
**Illustrative examples of supply curves and total supplies for fossil resources in GCAM **
{: .fig}

#### Representation of unconventional oil as a technology within crude oil

Unconventional oil and crude oil are merged into 1 resource (crude oil). Note that the ability for countries to produce unconventional oil is maintained by adding it as a subresource and technology within crude oil. This structure allows GCAM to load all costs and energy inputs related to unconventional oil production directly as technology costs. Since unconventional oil is combined with crude oil,they share a single price that governs supply expansion.   

### Renewable Resources

#### Wind

The supply curves in each region are derived from bottom-up analysis documented in [Zhou et al. (2012)](details_energy.html#zhou2012).

<img src="gcam-figs/wind.jpeg" width="900" height="500" /><br/>
**Illustrative example of global gridded potential for wind electricity generation used in GCAM **
{: .fig}

#### Solar

Distributed PV capacity factors are scaled across GCAM regions by the average latitude tilt irradiance for that region. The average latitude tilt irradiance for each country is derived from the "Latitude Tilt Radiation" variable from the NASA Surface meteorology and Solar Energy (SSE) Release 6.0 Data Set and averaged for each GCAM region. Forest and cropland areas are excluded.

The "distributed_PV" supply curve is of the same functional form as the wind supply curve, with an upward-sloping function designed to capture the increases in costs with deployment. In the USA region, the distributed_PV supply curve is estimated from data compiled by [Denholm (2008)](details_energy.html#denholm2008). The curve-exponent is assumed the same in all other regions, the mid-prices are adjusted according to the irradiance in each region, and the maxSubResources are adjusted according to the estimated building floorspace.

Concentrated Solar Power (CSP) capacity factors across GCAM regions depend on Direct Normal Irradiance (DNI), which is also derived from the the NASA SSE Release 6.0 Data as described in [Zhang et al. (2010)](details_energy.html#zhang2010). Areas with more than 200 days of low DNI (e.g., cloudy days) are excluded as these are not suitable for large-scale CSP installations. High latitude areas (> 45°) are excluded because DNI data was not available.

#### Geothermal

An additional XML file with Enhanced Geothermal Resources (EGS) is included with the standard GCAM input fileset, but is not included in the default configuration file. EGS expands the geothermal resource base significantly, albeit at higher costs, but is excluded from the default configuration due to the uncertainties about the future availability, effectiveness, and potential costs and risks of the technology.

## Energy Transformation

In energy transformation sectors, the output unit and input unit are EJ (per year), the price unit is 1975$ per GJ of output, and the subsector nest is used for competition between different fuels (or feedstocks). The competition between subsectors takes place according to a calibrated logit sharing function, detailed in [choice function](choice.html). Within the subsectors, there may be multiple competing technologies, where technologies typically represent either different efficiency levels, and/or the application of carbon dioxide capture and storage (CCS). The parameters relevant for technologies in GCAM are identified and explained in [energy technologies](en_technologies.html).

In the schematic of the energy system depicted below, the energy transformation and distribution sectors include all sectors except for the resources (colored red) and the final demands (colored light blue).

<img src="gcam-figs/energy_system_structure.jpg" width="900" height="650" /><br/>
**Simplified schematic of the energy system in each region, showing the inter-sectoral flows of energy goods in GCAM.**
{: .fig}

### Electricity

The nesting structure of the electric sector is shown in the figure below, with a focus on one repesentative technology.

<img src="gcam-figs/elec_structure.png" width="900" height="200" /><br/>
**Schematic showing the nesting structure of the electric sector, with levels for choices between fuels, technologies, and cooling systems. Note that this is a simplification of the actual structure used, which includes "pass-through" sectors, because GCAM sectors are only allowed two levels of nesting.**
{: .fig}

Details on the assumptions used in GCAM (e.g., cost, efficiency, capacity factors, etc.) is documented in [Muratori et al. 2017](energy.html#muratori2017). GCAM also includes the water inputs to electricity generation, in a third nest, as shown in the figure above. That is, within any thermo-electric generation technology, there is modeled competition between up to five different cooling system types; this is documented in the [water demand section](demand_water.html).

### Refining

The structure of refining in the broader energy system is shown in the following figure, with example input-output coefficients.

<img src="gcam-figs/refining.png" width="400" height="300" /><br/>
**Structure of refining sector and associated products within the energy system, with sample input-output coefficients shown. Electricity and natural gas inputs to oil refining not shown for simplicity.**
{: .fig}

#### Oil Refining

In a typical region, the oil refining technology consumes three energy inputs: crude oil, natural gas, and electricity. This is depicted graphically below, with typical input-output coefficients shown.

<img src="gcam-figs/oil_refining.png" width="300" height="150" /><br/>
**Oil refining production technology, with example coefficients.**
{: .fig}

#### Biomass Liquids

The biomass liquids subsector includes up to eight technologies in each region, with a global total of 11, listed in Table 1.

**Table 1: Biomass liquids production technologies in GCAM**
{: .tbl}

| Technology        | Inputs           |
| :------------- |:-------------|
| biodiesel (soybean)     | OilCrop, natural gas |
| biodiesel (oil palm)     | PalmFruit |
| biodiesel (Jatropha)     | biomassOil |
| cellulosic ethanol      | biomass      |
| cellulosic ethanol CCS level 1 | biomass      |
| cellulosic ethanol CCS level 2 | biomass      |
| corn ethanol      | Corn, natural gas, electricity |
| sugar cane ethanol      | SugarCrop |
| FT biofuels      | biomass |
| FT biofuels CCS level 1      | biomass |
| FT biofuels CCS level 2      | biomass |

### Gas Processing

The structure of the natural gas supply and distribution in GCAM is shown below:

<img src="gcam-figs/gas_processing.png" width="300" height="300" /><br/>
**Gas processing and distribution, with example coefficients.**
{: .fig}

Note that in this structure, biogas and coal gas compete for market share of the "gas processing" market, which is upstream of the gas pipeline and distribution sectors. This structure is intended to allow for substitution away from natural gas as the feedstock for the gaseous fuels used by the energy transformation and consumption sectors, as determined by the relative economics.


Note however that the following sectors consume natural gas upstream of the network shown in the figure above: unconventional oil production, gas-to-liquids refineries, and central hydrogen production. The gas used by these three processes is not assigned the cost mark-ups or upstream pipeline losses assumed in other industrial or energy sector consumers, and there is no capacity for the model to supply the gas used for these purposes with coal- or biomass-derived gas.

### District Services

In regions where purchased heat accounts for a large share of the final energy use, GCAM does include a representation of district heat production, with four competing technology options, shown below.

<img src="gcam-figs/district_heat.png" width="400" height="300" /><br/>
**District heating structure, with example input-output coefficients shown.**
{: .fig}

As shown, all energy losses and cost mark-ups incurred in transforming primary energy into delivered district heat are accounted in the "district heat" technologies; there are no explicit cost adders and efficiency losses for heat distribution, or different prices for the heat consumed by buildings and industry sectors. This simplistic representation reflects the lack of data on district heating globally, and that the delineation of what constitutes a "third party sale" as opposed to on-site use is often unclear. This is illustrated further in the graphic below.

<img src="gcam-figs/IEA_pulp_paper.png" width="450" height="350" /><br/>
**Energy flows in the pulp and paper industries, illustrating the delineation between energy producers and energy consumers. These components may or may not be located on the same property, or owned by the same entity, and the physical flows themselves often include backflows of combustible wastes from the "consumers" to the "producers". This complicates the accounting of what constitutes a "third party" sale of heat. Source: [IEA (2007)](energy.html#iea2007)**
{: .fig}

Another accounting issue that pertains to district heating is that the regions where it is represented also tend to have a large share, up to 100% in some years, of their district heat produced at "main activity CHP plants", which are modeled in the electricity sector in GCAM (see  [IEA Mapping](details_inputs.html#mapping-the-iea-energy-balances)). These are combined heat and power facilities whose primary purpose is sale of heat and/or electricity to third parties. In regions where heat is modeled as an energy commodity, the heat output of these main activity CHP plants is treated as a secondary output, and added to the total district heat produced in the given region. In future years, any new installations in the power sector are not assigned this secondary output of district heat; over time, these two sectors are modeled separately.

### Hydrogen

The structure of the hydrogen production and distribution sectors and technologies in GCAM generally uses the structure of the U.S. Department of Energy's Hydrogen Analysis (H2A) models [DOE 2015](details_energy.html#doe2015), and is shown in the figure below.

<img src="gcam-figs/hydrogen.png" width="600" height="400" /><br/>
**Hydrogen structure, with example input-output coefficients shown.**
{: .fig}

As in the H2A model [IHA 2000](details_energy.html#iha2000), the production of hydrogen takes place in two distinct sectors: H<sub>2</sub> Forecourt Production (i.e., on-site generation) and H<sub>2</sub> Central Production. The hydrogen produced at central facilities incurs additional cost mark-ups to reflect the distribution costs, whereas forecourt production typically entails higher energy intensities on the production side, and higher per-unit costs. Central production also has a greater diversity of feedstock options, described below.

The most common hydrogen production technology today is natural gas steam reforming, though coal chemical transformation is the dominant technology in China [IEA 2007](details_energy.html#iea2007). In GCAM, all regions have access to all technologies when hydrogen as an energy carrier becomes available; as shown in the figure above, hydrogen can be produced from up to 7 primary energy sources. Three of these sources (coal, gas, and biomass) include production technologies with CCS, characterized by higher costs and higher energy intensities, but lower CO<sub>2</sub> emissions.

The wind and solar technologies are electrolysis technologies, but are specifically disaggregated because these uses of wind and solar energy do not incur any backup-related costs, unlike in the electricity sector where backup costs increase as a function of their share of total grid capacity (see [electricity](supply_energy.html#electricity)). In contrast, the nuclear technology represents thermal splitting, which does not use electricity as an intermediate energy product.

## Trade

### Fossil fuel trade

 The figure below depicts the fossil fuel trade structures (using coal as an example). In previous versions of GCAM, every region produced and consumed from a single global market. All crude oil, coal, and natural gas production was sent to a shared market, from which, every region consumed. Only net trade could be tracked and supply was affected by global rather than regional demand. The current structure maintains a global market (e.g. traded coal), but distinguishes between direct consumption of domestic resources and consumption of imported fossil fuels.
 
<img src="gcam-figs/Fossil_fuel_trade.png" width="900" height="400" /><br/>
**Schematics of the structures for the flows of the "Coal" commodity in GCAM, with only 3 regions shown for simplicity.**
{: .fig}

#### Data calibration for fossil fuel trade

Each region's share of the global (e.g. traded coal) market as well as the split for domestic and imported goods are calibrated in the final base year. IEA's data set cannot be used to make this calibration because it lacks a bilateral trade accounting. Instead the GCAM data system uses the UN's Comtrade data set to account for intraregional trade to avoid double counting any gross trade. For example trade done within an aggregated GCAM region (e.g. Germany trading with France both of which are in GCAM's EU-15 region) should not be counted as part of that region's gross trade. To avoid overestimating the amounts of gross trade, Comtrade's bilateral data set is used to exclude any intraregional trade. The Comtrade trade data is used to calculate gross trade for each region. This is then combined with the data on production and consumption of fossil fuels calculated within the data system (production is calculated from the fossil fuel supply curves and IEA data and consumption is initialized from IEA energy balances) to compute trade balances. These trade balances are then used to initialize data for the domestic and traded sectors using relevant shareweights and interpolation rules.

## References

<a name="denholm2008">[Denholm 2008]</a> Denholm, P. 2008. *Supply Curves for Rooftop Solar PV-Generated Electricity for the United States*, Technical Report NREL/TP-6A0-44073, National Renewable Energy Laboratory. [Link](http://www.nrel.gov/docs/fy09osti/44073.pdf)

<a name="doe2015">[DOE 2015]</a> U.S. Department of Energy. 2015. *DOE H2A Production Analysis*, DOE Hydrogen and Fuel Cells Program. [Link](https://www.hydrogen.energy.gov/h2a_production.html)

<a name="iea2007">[IEA 2007]</a> International Energy Agency, 2007, *Tracking Industrial Energy Efficiency and CO<sub>2</sub> Emissions*, International Energy Agency, Paris, France. [Link](https://www.iea.org/publications/freepublications/publication/tracking_emissions.pdf)

<a name="iha2000">[IHA 2000]</a> International Hydropower Association, et al., 2000, *Hydropower and the World's Energy Future*. [Link](http://www.ieahydro.org/media/ffab53b0/Hydropower%20and%20the%20World's%20Energy%20Future%20.pdf)

<a name="zhang2010">[Zhang et al. 2010]</a> Zhang, Y., SJ Smith, GP Kyle, and PW Stackhouse Jr. (2010) Modeling the Potential for Thermal Concentrating Solar Power Technologies *Energy Policy* 38 pp. 7884–7897. [Link](https://doi.org/10.1016/j.enpol.2010.09.008)