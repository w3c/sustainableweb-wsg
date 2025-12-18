# Website Carbon Measurement

# Executive Summary

Website carbon emission measurement has evolved significantly over the past few years. Today, the dominant methods for website carbon emissions measurements are the Sustainable Web Design Model v4 and, increasingly, the Software Carbon Intensity (SCI) standard adoption. However, both of these methods have significant limitations. Page weight is an imperfect proxy for emissions, and the SCI standard lacks specific guidance for web-specific applications. Here we’ll explore the current state of the art, compare the competing methodologies and point out opportunity areas where the SCI for Web might focus.

## 1\. The Current Industry Standard

### Sustainable Web Design Model v4

The Sustainable Web Design Model (SWDM) v4, released July 2024, represents the current industry standard for website carbon calculations. It sums the contributions from three components to yield a website carbon emissions score in units of gCO2e/page view:

- **Data centers**: 22% of system energy (290 TWh globally) \- 82% operational, 18% embodied emissions  
    
- **Networks**: 24% of system energy (310 TWh) \- 82% operational, 18% embodied emissions  
    
- **User devices**: 54% of system energy (421 TWh) \- 49% operational, 51% embodied emissions

Version 4's calculation formula is as follows:

```
Average Emissions per Page View (gCO2e) = 
[(OPDC × (1 - Green Hosting Factor) + EMDC) + (OPN + EMN) + (OPUD + EMUD)] × New Visitor Ratio) + ([(OPDC × (1 - Green Hosting Factor) + EMDC) + (OPN + EMN) + (OPUD + EMUD)] × Return Visitor Ratio × (1 - Data Cache Ratio))

Where:

OPDC – Operational Emissions Data Centers.
Green Hosting Factor – The portion of hosting services powered by renewable or zero-carbon energy, between 0 and 1 (see FAQ).
EMDC – Embodied Emissions Data Centers.
OPN – Operational Emissions Networks.
EMN – Embodied Emissions Networks.
OPUD – Operational Emissions User Devices.
EMUD – Embodied Emissions User Devices.
New Visitor Ratio – The portion of first time visitors to a web page, between 0 and 1.
Return Visitor Ratio – The portion of returning visitors to a web page, between 0 and 1. (What is this? See FAQ)
Data Cache Ratio – The portion of data that is loaded from cache for returning visitors, between 0 and 1. (What is this? See FAQ)

```

Emissions estimates were reduced by 60-66% in Version 4 compared to Version 3\. Despite being the industry standard, SWDM v4 has faced criticism, especially around the suitability of page weight as a predictor of actual carbon emissions (e.g. [DebugBear, 2024](https://www.debugbear.com/blog/website-carbon-emissions)). 

Other methodologies include the OneByte model, originating from The Shift Project, which offers simplicity but excludes significant emission sources. DIMPACT, developed by University of Bristol with industry partners, provides the most data-driven approach but requires a lot of data disclosure, which in turn relies upon extensive partner cooperation. The SCI standard is arguably the most comprehensive framework but it was designed for general software rather than websites, meaning it is lacking in specific guidance for measuring web applications.

## 2\. Alternative Methodologies Comparison

### Methodology Landscape

The following table compares the main methodologies used to measure website carbon emissions today.

| Dimension | SWDM v4 | OneByte Model | DIMPACT | SCI (ISO/IEC 21031:2024) |
| :---- | :---- | :---- | :---- | :---- |
| **Scope & Boundaries** | Cradle-to-grave: data centers, networks, user devices | Gate-to-gate: data centers and networks only | Complete digital media value chain | Flexible boundaries defined per software system |
| **Primary Metric** | CO2e per page view | CO2e per byte transferred | Process-based emissions per media asset | Carbon intensity per functional unit |
| **Formula Complexity** | Multi-factor with cache ratios and visitor types | Linear: Data × Energy × Carbon intensity | Activity-based with detailed process mapping | SCI \= ((E × I) \+ M) per R |
| **Embodied Emissions** | Included: 18% for infrastructure, 51% for devices | Excluded | Included through detailed equipment inventory | Included (M component) with time/resource allocation |
| **Functional Units** | Fixed: per page view | Fixed: per GB transferred | Flexible: per hour viewed, per asset delivered | Flexible: per user, transaction, API call, etc. |
| **Energy Data Source** | Global averages: 0.055-0.080 kWh/GB by segment | Fixed: 0.06 kWh/GB (2018 data) | Actual measurements from partners | Real telemetry or lab measurements |
| **Carbon Intensity** | Global average: 494g CO2e/kWh | User-selectable or global average | Regional grid factors | Location-specific, excludes market measures |
| **Caching Consideration** | 75% new, 25% return with 98% cache efficiency | Not considered | Detailed CDN modelling | Not specified |
| **Green Hosting** | Includes green hosting factor | Not considered | Actual energy sourcing data | Excludes renewable certificates |
| **Validation Method** | Industry review, no empirical validation | Academic origin, limited validation | Industry \+ academic validation | Requires measurement documentation |
| **Best Use Case** | General website assessment | Quick estimates, browser extensions | Media streaming and broadcasting | Software applications with clear boundaries |
| **Key Limitation** | Page weight as imperfect proxy | Oversimplified, outdated factors | Complex data requirements | Requires adaptation for web contexts |

## 3\. Refining the SCI Standard for Web

The Software Carbon Intensity (SCI) standard (ISO/IEC 21031:2024) is calculated as:

**SCI \= ((E × I) \+ M) per R**

Where:

- E \= Energy consumed by software system (kWh)  
- I \= Location-based carbon intensity (gCO2eq/kWh)  
- M \= Embodied carbon emissions from hardware  
- R \= Functional unit (per user, transaction, request)

### 

The SCI has some key advantages over competing methodologies, including a scope that encompasses operational energy, carbon intensity, AND embodied emissions, flexibility in functional unit choice, an unopinionated approach to the route users take to measure E, I, M and R, exclusion of offsets (no “market based” measures allowed), detailed handling of hardware and recognition from ISO.

However, the SCI specification is designed to apply broadly to all software, meaning there is a lack of particular guidance for websites. Some of the key areas of uncertainty are

**Functional Unit Definition**: There are many units that could be appropriate for expressing website carbon emissions, for example page views, unique visitors, MAU, transactions, content delivery, API calls, etc. SCI does not currently give guidance regarding which functional units are appropriate for different web use cases.

**Boundary Determination**: Modern websites are served on complex distributed infrastructure, including third-party scripts, CDNs, external APIs, client/server processing splits, and progressive web apps. SCI does not define where the system boundary lies.

**Energy Measurement**: Users often have limited access to actual consumption data, especially in shared hosting environments, serverless architectures, etc, and SCI does not suggest appropriate proxies or methodologies for converting those proxies into energy estimates.

**Embodied Emissions**: It is difficult to determine the appropriate physical resource-share for websites using shared infrastructure and user devices running thousands of applications. SCI currently only gives high level instructions for amortizing hardware emissions.

## 4\. Opportunities for SCI for Web

Based on the uncertainties identified above, these are some potential valuable deliverables for SCI for Web:

- Provide a rubric for choosing an appropriate functional unit that addresses the main web architectures.  
- Define an appropriate system boundary. Make it clear what components are in/out of scope for an SCI measurement.  
- Provide a hierarchy of proxy data sources and recommended methodologies for converting them into E, I, M or R.  
- Clarify the allocation strategy for hardware emissions, including for complex shared resources.  
- Include a degree of cache-awareness.Differentiate new vs returning visitor impacts, account for CDN hit rates, browser caching etc.

These could then be wrapped in the language of the SCI specification for submission to ISO.

## 5\. SCI for Web case study

**Cardamon**, developed by Root & Branch Digital, pioneered the first website measurement tool explicitly built to comply with the SCI standard (ISO/IEC 21031:2024). 

Key features of Cardamon's SCI implementation:

1. **Scenario-based measurement**: Cardamon is built around the concept of observations and scenarios. A scenario encapsulates a usage behaviour that you want to measure (e.g. add items to basket), compatible with ISO/IEC 21031 \- Software Carbon Intensity (SCI) specification.  
     
2. **Real power consumption tracking**: Unlike tools relying on data transfer proxies, Cardamon collects data every 2 seconds to measure actual power consumption of software processes, including Docker containers and bare-metal applications.  
     
3. **Functional unit flexibility**: Scenarios can represent any user behaviour, allowing measurement per transaction, per user action, or custom functional units as required by SCI.  
     
4. **Configuration-based approach**: Uses a `cardamon.toml` file to define:  
   * CPU specifications with average power consumption  
   * Processes to measure (Docker or bare-metal)  
   * Scenarios representing user behaviours  
   * Observations combining scenarios and processes  
       
5. **Iterative measurement**: Scenarios can be run multiple times to take an average, improving accuracy of carbon intensity calculations.

This implementation addresses several SCI adaptation challenges for websites by providing scenario-based functional units, actual energy measurement rather than proxies, and support for distributed architectures through Docker container tracking. It is probably well worth engaging the developers of Cardamon to benefit from their experiences and understand their design decisions as we develop SCI for Web.