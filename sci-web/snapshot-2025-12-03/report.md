# SCI for Web - Assembly Report

**Status**: Draft Report from Assembly Process  
**Version**: 1.0  
**Date**: [Date]  
**Contributors**: [List of assembly participants]

---

## Executive Summary

[Brief 2-3 paragraph overview of the assembly process, key decisions made, and the path forward to formal specification development]

---

## 1. Scope Definition

**Purpose**: This section defines what constitutes a "web application" for the purposes of SCI for Web measurement. It answers the question: "For whom and for which scenarios, use cases, applications, and audiences is this specification intended?"

**What this section contains**:
- Clear definition of "web application" based on architectural characteristics and interaction patterns
- Principles for determining whether an application falls within scope
- Statement of what is explicitly out of scope (e.g., native mobile applications, desktop software)

**What this section does NOT contain**:
- Lists of infrastructure components (servers, CDNs, databases)
- Calculation methodologies or formulas
- Classification of specific boundary cases or edge cases
- Measurement procedures or implementation guidance

**Constraints**:
- Must align with parent SCI specification (cannot contradict SHALL/MUST/SHOULD requirements)
- Must be narrow enough to be actionable, broad enough to cover legitimate use cases
- Must represent consensus position from assembly participants

---

The SCI for Web specification applies to software applications that deliver functional value to human users primarily through browser-based interfaces accessed via HTTP/HTTPS protocols. A web application is characterized by three essential criteria: (1) content and functionality delivered over HTTP/HTTPS protocols, (2) rendering and execution occurring primarily within web browser environments or equivalent web rendering engines, and (3) interfaces designed for direct human interaction and consumption rather than exclusively machine-to-machine communication.

The scope encompasses the full spectrum of browser-based applications regardless of architectural sophistication, including static content websites, dynamic platforms, single-page applications (SPAs), server-side rendered applications, e-commerce systems, media streaming services, and real-time collaborative tools. The distinguishing principle is browser-mediated human interaction: if users primarily access functionality through web browsers to accomplish tasks or consume content, the application falls within scope. This definition is intentionally platform-independent and technology-agnostic, focusing on delivery mechanism and user interaction patterns rather than specific implementation technologies.

API-driven services require additional classification based on their primary access pattern. Pure machine-to-machine APIs serving only programmatic clients are out of scope and should use the base SCI methodology. However, APIs accessed primarily through browser-based interfaces—such as those with interactive documentation as the primary usage method or those coupled with browser-based management dashboards—fall within scope when the browser interface represents the primary human interaction mode. The determining factor is whether human users consume the service's value through browser rendering, not whether HTTP protocols are involved.

---

## 2. Target Personas

**Purpose**: This section identifies the professional roles and organizational actors who should use this specification and whose behavior the measurement framework aims to influence.

**What this section contains**:
- Primary professional roles (e.g., sustainability engineers, frontend developers, DevOps engineers, product managers)
- Secondary stakeholders (e.g., procurement officers, compliance teams, executives)
- Organizational contexts where SCI for Web applies (e.g., SaaS providers, e-commerce platforms, media companies)
- How different personas will use the specification (optimization decisions, reporting, vendor selection)
- Decision-making power each role has (what they control vs. don't control)
- Current barriers preventing them from prioritizing carbon

**What this section does NOT contain**:
- End-user personas (consumer vs. business users of web applications)
- Geographic or demographic segmentation
- Marketing or communications strategies

**Why this matters**:
We must know WHO we want to influence before we can design incentives or evaluation criteria. These personas have agency to reduce web carbon through their decisions.

**Connection to other sections**:
- Drives Behavioral Incentives (Section 3) - we design incentives for these specific roles
- Informs Evaluation Criteria (Section 4) - we evaluate based on whether design serves these personas
- Justifies Scope Definition (Section 1) - scope must be relevant to personas' work

**Process note**: This section will be developed through consensus-building based on assembly discussions about who has agency to improve web application sustainability and who needs measurement frameworks to guide decisions.

---

The SCI for Web specification is designed for **technical practitioners who create and optimize browser-mediated web applications**, spanning both server-side infrastructure and client-side implementation. Because the agreed scope defines web applications through "browser-mediated human interaction via HTTP/HTTPS," the specification must serve personas who control energy consumption across the entire delivery chain—from servers generating responses to browsers rendering content for human users.

### **Frontend Developers and Design Practitioners**

These practitioners control the code, assets, and experiences delivered to browsers, directly affecting energy consumed on end-user devices during browser-mediated interactions. This includes:

- **Frontend developers**: JavaScript bundle size and optimization, CSS efficiency, framework selection for client-side execution, third-party script integration, rendering performance, asset optimization (images, fonts, videos), progressive enhancement strategies, and client-side caching
- **UX/UI designers**: Interface design decisions affecting resource consumption (infinite scroll vs. pagination, video backgrounds vs. static images, auto-playing media), interaction patterns determining data transfer frequency, content structure and information architecture
- **Content designers**: Content strategy affecting page weight, media selection and optimization requirements, structured content delivery

**What they control**: Client-side code efficiency, browser rendering performance, third-party client-side dependencies, asset delivery and optimization, user interaction patterns, content weight and structure, design decisions with 10x+ energy impact potential

**What they don't control**: Server-side infrastructure location, database architecture, hosting provider selection, network infrastructure between datacenter and user, end-user device hardware specifications

### **Backend and Infrastructure Engineers**

These practitioners control server-side systems that generate and deliver content to browsers, affecting operational emissions from datacenters and infrastructure. This includes:

- **Backend developers**: Server-side code efficiency, API design and optimization, database query performance, caching strategies, session management
- **Infrastructure and systems engineers**: Cloud provider and geographic hosting location selection, server capacity planning and right-sizing, resource utilization policies, infrastructure architecture (static vs. dynamic provisioning), build and deployment pipeline efficiency (CI/CD, testing, artifact storage)
- **Platform and DevOps engineers**: CDN configuration and edge caching, architectural patterns affecting server/client computation distribution (server-side rendering, static site generation, hybrid approaches), monitoring and observability systems, performance optimization tooling

**What they control**: Server-side compute and storage resources, database efficiency and architecture, geographic hosting location and carbon intensity exposure, infrastructure capacity relative to actual traffic, deployment and build processes, caching at server and CDN levels, API efficiency

**What they don't control**: End-user device choices, browser vendor implementations, client-side third-party script behavior (though can control whether to include them), market-based carbon offsets (excluded from SCI methodology)

### **Product Owners and Technical Managers**

These practitioners translate organizational goals into technical requirements and manage trade-offs between features, performance, and sustainability. This includes:

- **Product owners and managers**: Feature prioritization and lifecycle management ("gardening"—pruning unnecessary features), performance budget setting, sustainability target definition, trade-off decisions between functionality and efficiency
- **Technical leads and architects**: Architectural decision-making authority, technology selection across the stack, team capacity allocation for optimization work, supplier and third-party service selection criteria, non-functional requirements including performance and sustainability

**What they control**: Which features get built and maintained, performance and sustainability budgets, team time allocation for optimization, supplier selection based on sustainability criteria, architectural standards and patterns

**What they don't control**: Day-to-day implementation details, supplier internal implementations (though can switch suppliers), end-user behavior and device choices, industry-wide standards (though can advocate)

### **Rationale: Connection to Scope**

The agreed scope defines web applications as "browser-mediated human interaction" where "rendering and execution occur primarily within web browser environments." This explicitly requires measuring both server-side energy (generating responses) and client-side energy (rendering for human interaction). Frontend practitioners who control browser-delivered experiences are therefore equally essential to backend practitioners who control server infrastructure. Product roles provide the decision-making authority to prioritize sustainability work and set performance budgets that enable technical implementation.

### **Critical Inclusion: Third-Party Dependencies and Transparency**

Modern web applications depend extensively on third-party services for functionality (analytics, advertising, authentication, payments, CDNs, hosting). These dependencies consume energy on both servers and client devices. **Third-party services must be included within the SCI for Web boundary** to incentivize measurement, monitoring, and improvement of their performance and energy efficiency, encouraging them to reduce their own carbon emissions. Measurement and monitoring also provides the necessary data to make informed decisions about when and whether to select third-party services over first-party implementations.

When precise energy data from third-party suppliers is unavailable, practitioners shall use industry default values with explicit disclosure that estimates were used. This approach balances comprehensiveness with implementation feasibility while creating market pressure for suppliers to provide transparency.

**Supplier influence mechanism**: While practitioners cannot directly control third-party implementations, they exercise influence through vendor selection, contractual requirements for emissions transparency, and the collective market signal that sustainability performance affects purchasing decisions.

### **Acknowledged but Not Primary Targets**

**Suppliers and third-party service providers**: While their implementations significantly impact web application carbon footprint, they are users of this specification rather than its primary audience. The specification enables practitioners to pressure suppliers for transparency and better performance through informed vendor selection.

**Standards bodies and regulatory authorities**: These entities set the broader context but are not the specification's implementation audience. The specification should align with existing standards (parent SCI methodology, accessibility guidelines) and support regulatory compliance without targeting these bodies as primary users.

**End users and consumers**: These individuals have limited agency based on choices made by practitioners. User-facing interventions (sustainable mode toggles, carbon-aware delivery options) depend on practitioner implementation and are better addressed through choice architecture design than direct user targeting.

---

## 3. Implementation Practices and Incentives

**Purpose**: This section documents what practices and optimizations the SCI for Web measurement framework encourages and discourages. It explains the design choices that align carbon reduction with business value and prevent perverse incentives.

**What this section contains**:
- **Desired practices**: Efficiency improvements, architectural optimizations, responsible vendor selection, quality-preserving carbon reduction
- **Perverse incentives to avoid**: Quality degradation, cost-shifting to users, vanity metrics, gaming measurements
- **Design choices**: How functional unit selection, boundary definitions, and measurement methodologies create proper incentives
- **Trade-offs**: How the framework balances competing goals (accuracy vs. simplicity, comprehensiveness vs. feasibility)

**Why this matters**:
Measurement frameworks shape practices. If we measure the wrong things or measure them poorly, we incentivize harmful optimizations. This section makes explicit the practices and incentives underlying SCI for Web design.

**Connection to other sections**:
- Follows from Target Personas (Section 2) - we incentivize the identified professional roles
- Informs Evaluation Criteria (Section 4) - evaluation assesses whether design achieves these incentives
- Justifies Scope Definition (Section 1) - scope choices have implications for practices and incentives

**Process note**: This section will be developed through consensus-building based on assembly discussions about optimization strategies, measurement concerns, and desired outcomes. It will also inform FAQ entries explaining why certain design choices were made.

---

This section defines the specific practices that SCI for Web should encourage or discourage in teams who measure and optimize web applications. These implementation practices guide design decisions throughout the specification, ensuring that measurement drives genuine carbon reduction rather than metric optimization.

**Implementation Note**: While this section describes comprehensive practices across all system components, teams may adopt SCI for Web incrementally. Starting with measurable components (client-side and server-side infrastructure under direct control) and progressively expanding scope to include network transfer and third-party services is an acceptable path to comprehensive measurement. However, disclosed methodology must clearly identify which components are measured versus estimated versus excluded to maintain transparency and prevent gaming.

**Note on Principles vs. Prescription**: The practices described below represent principles and patterns that reduce energy consumption. They are not prescriptive engineering requirements. Teams should evaluate these principles within their specific context and implement them using approaches appropriate to their architecture, constraints, and objectives.

## Encouraged Practices

### For Frontend Developers and Design Practitioners

**Energy reduction outcomes targeted**: Reduce data transfer, reduce page weight, reduce client-side energy consumption, extend end-user device lifespan, reduce CPU/GPU utilization during rendering.

**Energy reduction practices to encourage:**

- **Optimize asset delivery**: Reduce bundle sizes, compress assets appropriately (images, videos, PDFs, audio files, and other media), eliminate unused CSS and JavaScript, implement code splitting, lazy-load non-critical resources
- **Choose efficient rendering approaches**: Use progressive enhancement, implement server-side rendering or static generation where appropriate, minimize client-side computation for tasks that could run more efficiently on servers
- **Design for efficiency**: Favor text over video or decorative image backgrounds, implement pagination over infinite scroll where appropriate, avoid auto-playing media, optimize animation performance, design effective user workflows that minimize unnecessary interactions
- **Reduce third-party dependencies**: Minimize analytics scripts, advertising trackers, and external fonts; evaluate whether each third-party service provides sufficient value for its energy cost
- **Optimize for diverse devices**: Test on low-end devices, implement responsive images, ensure experiences work efficiently across device capabilities
- **Inform users**: Provide transparency about the environmental impact of using or overusing certain features, such as reverse logistics in e-commerce or continuous rendering of intensive visual assets

**How these practices reduce energy:** Client-side optimizations directly reduce energy consumed on end-user devices (operational) and can extend device lifespan (embodied). Smaller data transfers reduce network energy. Efficient rendering reduces CPU/GPU utilization and battery drain. User transparency enables informed decision-making about feature usage.

### For Backend and Infrastructure Engineers

**Energy reduction outcomes targeted**: Minimize server-side resource usage, reduce datacenter electricity consumption, reduce CPU/memory/storage utilization, reduce network transmission distance and carbon intensity exposure.

**Energy reduction practices to encourage:**

- **Right-size infrastructure**: Match server capacity to actual load, avoid over-provisioning, implement auto-scaling that responds to real demand, decommission unused services, optimize underlying infrastructure choices such as VM instance types and image sizes
- **Optimize database and API efficiency**: Design efficient database schemas, write efficient queries, implement appropriate indexing, reduce unnecessary data fetching, cache effectively, eliminate N+1 query patterns
- **Choose efficient hosting**: Select hosting providers and regions based on carbon intensity and renewable energy availability, use edge computing to serve users from geographically closer locations
- **Architectural efficiency**: Implement effective caching strategies (CDN, server-side, database), use content delivery networks appropriately, select efficient technology stacks
- **Measure and monitor resource utilization**: Track actual CPU, memory, and storage usage; identify and eliminate wasteful operations; implement benchmarking during development and production phases

**How these practices reduce energy:** Server optimizations directly reduce datacenter electricity consumption. Right-sizing reduces both operational energy and embodied emissions from idle hardware. Geographic hosting choices reduce both transmission distance and exposure to carbon-intensive grids. Benchmarking during development catches inefficiencies before production deployment.

### For Product Owners and Technical Managers

**Energy reduction outcomes targeted**: Prevent feature bloat that increases page weight and server load, establish performance constraints that limit energy consumption, incentivize vendor efficiency improvements through market pressure.

**Energy reduction practices to encourage:**

- **Practice "feature gardening"**: Regularly audit and remove low-value features that consume resources, resist feature bloat, prioritize quality over quantity
- **Set performance and environmental budgets**: Establish and enforce limits on page weight, JavaScript execution time, and API response times that implicitly constrain energy consumption; define environmental budgets that track sustainability KPIs such as energy use, waste, and CO2 emissions thresholds in alignment with frameworks like GRI
- **Make informed vendor decisions**: Select third-party services based on their efficiency and carbon transparency, require emissions data from vendors, switch to more efficient alternatives when available
- **Allocate optimization time**: Provide team capacity for performance and efficiency work, treat optimization as ongoing maintenance rather than one-time effort
- **Balance functionality with efficiency**: Make conscious trade-offs between feature richness and resource consumption, question whether new features justify their carbon cost
- **Make carbon efficiency a quality attribute**: Implement non-functional requirements for carbon emissions, measure them, and use them as quality gates in development processes
- **Prefer "always-available" over "always-on"**: Design systems so that resource-intensive features (like intensive rendering, data export, or batch processing) can be scheduled during low-carbon periods or rate-limited rather than running continuously at any time

**How these practices reduce energy:** Product and management decisions determine what gets built and maintained. Removing unused features eliminates ongoing server costs and client-side execution. Performance and environmental budgets prevent gradual efficiency degradation. Vendor transparency requirements create market incentives for supplier optimization. Carbon-aware scheduling reduces emissions by timing computation to periods of lower grid carbon intensity.

### For Third-Party Service Providers and Hosting Suppliers

**Energy reduction outcomes targeted**: Reduce energy consumption per operation across all customer implementations, enable informed vendor selection through transparency, reduce grid carbon intensity through renewable energy procurement.

**Energy reduction practices to encourage:**

- **Provide transparency**: Publish energy consumption and carbon emissions data for services, offer APIs for customers to access real-time or historical emissions data
- **Optimize implementations**: Invest in efficiency improvements that reduce energy per operation, implement efficient caching and content delivery
- **Support customer measurement**: Provide detailed metrics on resource consumption, enable customers to attribute emissions accurately
- **Procure renewable energy**: Procure renewable energy wherever possible for all energy-consuming activities. For datacenters, select low-carbon hosting locations and invest in energy efficiency improvements

**How these practices reduce energy:** Supplier optimizations cascade across all customers. Transparency enables informed vendor selection. Renewable energy procurement reduces carbon intensity exposure for all customer workloads.

## Discouraged Practices

### Energy Displacement Rather Than Reduction

**Practice to discourage:** Shifting computation from measured locations to unmeasured locations to improve metrics without reducing total system energy.

**Examples:**
- Moving computation from servers to client devices through heavy JavaScript to reduce measured server energy while increasing unmeasured client energy
- Outsourcing computation to third-party services to externalize emissions from first-party measurements
- Increasing build-time computation to reduce runtime computation (if development lifecycle is unmeasured)

**Why this matters:** Displacement makes metrics look better while total system energy stays the same or increases. This is measurement gaming, not carbon reduction.

**Design implication:** SCI for Web must measure comprehensively across servers, networks, third-party services, and end-user devices to close displacement pathways.

### Quality Degradation as "Optimization"

**Practice to discourage:** Reducing functionality, accessibility, security, privacy, or user experience to improve energy metrics.

**Examples:**
- Reducing image quality below acceptable thresholds to decrease data transfer
- Removing accessibility, security, or privacy features to reduce the website payload
- Limiting essential functionality to reduce computation
- Degrading user experience (e.g., removing helpful features) to improve scores

**Why this matters:** Measurements should incentivize delivering functionality efficiently, not delivering reduced functionality. Users accomplish the same tasks less efficiently or switch to less-efficient alternatives. Compromising accessibility, security, or privacy creates net harm that outweighs carbon benefits.

**Design implication:** Functional units should measure energy per delivered functionality, not energy per technical operation. Multidimensional metrics capture quality-efficiency trade-offs.

### Market-Based Measures Instead of Elimination

**Practice to discourage:** Using carbon offsets, renewable energy certificates (RECs), or other market-based instruments to improve scores without reducing actual energy consumption.

**Examples:**
- Purchasing carbon offsets to neutralize emissions while maintaining inefficient operations
- Buying RECs to claim "green" energy without reducing actual electricity use
- Geographic arbitrage where applications claim low emissions by measuring only low-carbon regions while serving global users

**Why this matters:** The parent SCI specification explicitly excludes market-based measures (see SPEC.md sections on Exclusions and Market-based Measures). The goal is eliminating emissions through efficiency, not compensating for inefficiency through financial instruments. As stated in the SCI specification: "Reducing an SCI score is only possible through the elimination of emissions."

**Design implication:** SCI for Web measures energy consumption and carbon intensity based on actual infrastructure location and operation, without adjustments for offsets or certificates. Carbon intensity calculations use location-based grid intensity, excluding market-based measures as defined in the parent specification.

### Measurement Gaming and Boundary Manipulation

**Practice to discourage:** Optimizing measurement boundaries and methodologies to improve scores without reducing actual emissions.

**Examples:**
- Selectively excluding high-emission components from measurement scope
- Choosing functional units that make inefficient operations appear efficient
- Reducing essential activities (testing, security updates) to improve operational metrics
- Cherry-picking measurement timeframes to avoid high-load periods

**Why this matters:** Gaming destroys measurement credibility and prevents comparability. Organizations compete on measurement skill rather than actual efficiency.

**Design implication:** Mandatory comprehensive boundaries, disclosed methodologies, and consistent functional units prevent gaming while allowing legitimate architectural diversity.

### Vanity Metrics and Proxy Optimization

**Practice to discourage:** Optimizing proxy metrics that correlate weakly with actual energy consumption.

**Examples:**
- Optimizing page weight without considering how assets are used (e.g., reducing rarely-loaded resources while ignoring frequently-loaded ones)
- Focusing on first contentful paint while ignoring total page energy consumption
- Reducing server response time by pushing computation to client without measuring total system impact
- Optimizing for synthetic benchmarks that don't reflect real user usage patterns

**Why this matters:** Proxy optimization can increase actual energy while improving measured proxies. Focus on proxies diverts attention from genuine efficiency improvements.

**Design implication:** Where possible, measure actual energy consumption rather than proxies. When proxies are necessary, validate correlation with real energy impact and use multiple dimensions.

## Design Implications for SCI for Web

These implementation goals inform specific design decisions:

**Comprehensive measurement boundaries:** To discourage displacement, SCI for Web must measure energy across servers, networks, third-party services, and end-user devices. Excluding any major component creates a displacement pathway.

**Functional units measuring delivered functionality:** To discourage quality degradation, functional units should capture delivered functionality (transactions, content consumed, tasks completed) rather than just technical operations (page views, API calls).

**Mandatory disclosure of methodologies:** To prevent boundary gaming, organizations must disclose what they measured, how they measured it, and what they excluded. This enables peer comparison and identifies gaming attempts.

**Operational serving focus:** To avoid perverse incentives in development practices (reduced testing, delayed security patches), measure operational serving efficiency separately from development lifecycle efficiency.

**Exclusion of market-based measures:** Following the parent SCI specification, SCI for Web excludes offsets, RECs, and other market-based instruments, focusing measurement on actual energy elimination through the three sustainability actions defined in the parent specification: energy efficiency, hardware efficiency, and carbon awareness.

**Tiered implementation with disclosed sophistication:** To encourage adoption while maintaining comprehensive boundaries, allow organizations to start with industry defaults and increase measurement sophistication over time, with mandatory disclosure of which tier methodology is used.

**Inclusion of embodied emissions:** To account for hardware manufacturing impacts and incentivize longer device lifespan and better resource utilization, include embodied emissions allocated proportionally to usage time, following the calculation methodology specified in the parent SCI specification.

**Third-party service transparency requirements:** To pressure vendors for efficiency improvements, require including third-party services with vendor-provided data where available or conservative proxy estimates where unavailable.

The overarching principle: SCI for Web design decisions should make practices that genuinely reduce total system energy the same practices that improve measured scores. When measurement and reality align, teams optimize actual efficiency rather than metrics.


---

## 4. Evaluation Criteria

**Purpose**: This section defines what makes SCI for Web measurement credible, trustworthy, and worth implementing. It addresses the fundamental tension in sustainability measurement: scientifically rigorous specifications that nobody implements vs. imperfect but widely adopted measurements that actually reduce carbon.

**What this section contains**:
- Trade-offs between measurement accuracy and implementation simplicity
- Trust and transparency requirements (what must be disclosed vs. what's optional)
- Threshold criteria for usefulness (minimum accuracy, maximum complexity)
- Gaming prevention principles (how to design out perverse incentives)
- Success indicators (how we'll know if SCI for Web achieves its goals)
- Implementation feasibility boundaries (what's too complex to expect adoption)

**What this section does NOT contain**:
- Detailed technical implementation specifications
- Specific tooling requirements or recommendations
- Prescriptive step-by-step procedures
- Maturity tier definitions (those belong in the formal specification)

**Why this matters**:
The sustainability space is full of specifications that are scientifically correct but unused. This section explicitly addresses the adoption-accuracy trade-off and establishes what "good enough" looks like. We evaluate SCI for Web based on whether it incentivizes target personas toward identified behaviors while remaining implementable.

**Key questions this section answers**:
- How accurate does measurement need to be to drive behavior change?
- How simple does implementation need to be for widespread adoption?
- What disclosure is required for credibility without killing adoption?
- What would make target personas reject or ignore SCI for Web?
- Does the measurement framework achieve the behavioral incentives we identified?

**Connection to other sections**:
- Follows from Behavioral Incentives (Section 3) - we evaluate based on whether design achieves those incentives
- Informed by Target Personas (Section 2) - evaluation considers implementability for those roles
- Enables Comparative Analysis (Section 5) - provides criteria for assessing SCI for Web vs. alternatives

**Process note**: This section will be developed through consensus-building based on assembly discussions about trust, implementation feasibility, and success criteria.

---

# Section 4: Evaluation Criteria - Merged Consensus Proposal

## Overview

This section establishes evaluation criteria for SCI for Web that balance scientific rigor with practical adoptability. The criteria recognize that unused specifications serve no one, while measurements lacking credibility undermine sustainability efforts. Our evaluation framework prioritizes defensible accuracy where teams have direct control, workflow integration over exceptional effort, and transparent limitations over false precision.

The fundamental tension: scientifically rigorous specifications that nobody implements versus imperfect but widely adopted measurements that actually reduce carbon. SCI for Web must navigate this trade-off by being accurate enough to drive meaningful behavior change while simple enough for widespread adoption.

## 1. The Accuracy-Adoption Trade-off

### Sufficient Accuracy for Behavior Change

SCI for Web does not require laboratory-grade precision to drive meaningful behavior change, but accuracy must be real, not merely perceived. Measurements inform decisions with carbon and ethical implications, making actual accuracy critical even as we acknowledge that perfect precision is unattainable.

**Accurate enough to be defensible**: Measurements should enable teams to make informed decisions about which approaches genuinely reduce carbon emissions. When comparing options or tracking changes over time (comparing version A to version B, or approach X to approach Y), teams need confidence that observed differences reflect reality. A measurement framework showing that one implementation approach has 20% higher energy consumption than another warrants investigation and drives optimization; a framework showing 50% variance for equivalent implementations creates confusion and mistrust.

The acceptable variance range depends on what teams have direct control over:
- **Directly measured components** (browser execution, server operations teams manage): measurements within 10-15% of actual consumption enable confident decision-making
- **Well-modeled components** with substantial real-world data backing (network transfer, user device diversity): measurements within 15-20% are acceptable as a starting point, with expectation of improvement as datasets grow
- **Components with limited data availability**: clearly labeled placeholders and estimates are acceptable when they are explicitly marked as such, based on best available data and reasonable assumptions, documented with clear methodology, and accompanied by a path to improvement

**Proportional to control and influence**: Accuracy requirements should scale with the degree of direct control teams have:
- High accuracy for directly controlled elements (browser rendering from code teams write, server operations they manage)
- Moderate accuracy for indirectly influenced elements (user behavior patterns, caching effectiveness, third-party services where vendor selection is controlled)
- Explicit acknowledgment of uncertainty for uncontrolled elements (network infrastructure beyond origin servers, diverse user device characteristics)

This proportionality principle aligns with the parent SCI specification's emphasis on actionable measurements that drive the three sustainability actions: energy efficiency, hardware efficiency, and carbon awareness.

**Grounded in measurable reality**: Where direct measurement is feasible, it should be the foundation. Where modeling is necessary, it should be backed by substantial datasets from real-world observations, not theoretical assumptions. This follows the parent SCI specification's guidance: "The SCI encourages calculation using granular real-world data" while allowing "data generated through modeling, using best estimates" when real-world data is unavailable.

### Implementation Simplicity for Widespread Adoption

The parent SCI specification establishes as a core characteristic that "The SCI is easy to implement" and that "anyone without much experience or training shall be able to follow the SCI specification instructions." SCI for Web must honor this principle while addressing web-specific complexity.

**Workflow integration**: The specification should work within existing tools and platforms—content management systems, CI/CD pipelines, analytics tools, monitoring systems. If adoption requires new toolchains separate from normal development workflows, it faces immediate organizational resistance. This aligns with Section 3's identified behavioral incentive: teams will only adopt measurement that integrates naturally into their existing practices.

**Automation and standardization**: Manual measurement invites inconsistency and abandonment. High degrees of automation lower entry barriers, making adoption possible across the diverse roles identified in Section 2 (frontend developers, DevOps engineers, product managers) without specialized sustainability training.

**Clear boundaries and minimal disruption**: Teams should understand exactly what they're measuring, why it matters, and what actions they can take. The specification should define clear scope boundaries that map to team responsibilities and capabilities identified in the Target Personas section.

**Progressive sophistication**: Teams at different capability levels and organizational contexts should be able to adopt SCI for Web appropriately. Entry-level adoption with simpler methodologies should be legitimate and valuable, with clear pathways to more comprehensive measurement as capabilities mature. (Note: specific maturity tier definitions belong in the formal specification, not this evaluation criteria section.)

## 2. Trust and Transparency Requirements

### Mandatory Disclosure

Credibility requires transparency about methodology, data sources, and limitations. The parent SCI specification requires that teams "Disclose the SCI score, software boundary, and the calculation methodology." SCI for Web extends this principle to web-specific contexts.

**Methodology and assumptions**: The calculation approach, models used, and assumptions made must be explicitly documented. When placeholders, estimates, or constants are used, they must be clearly identified as such with justification for the chosen values. This enables peer review and prevents hidden gaming.

**Data provenance**: Sources of data—whether from direct measurement, third-party services, reference devices, or public databases—must be disclosed. The chain from raw data to final calculation should be traceable. This follows the parent specification's emphasis on encouraging "the use of granular data."

**Measurement boundaries**: What is included and excluded from the measurement must be explicit, following the parent specification's software boundary guidance. If third-party services are excluded, state this. If measurements only apply to specific user journeys or geographic regions, say so. This prevents boundary gaming identified in Section 3 as a discouraged practice.

**Limitations and uncertainty**: Where accuracy cannot be assured, acknowledge it. Where control is limited, make it visible. Uncertainty ranges should be disclosed rather than hidden behind false precision. A single unconvincing component presented with false precision can discredit the entire framework.

**Quantification method disclosure**: Following the parent SCI specification's procedure, teams must disclose whether they used measurement (real-world data) or calculation (models) for each component, and with what level of sophistication. This transparency enables comparability and prevents gaming through selective methodology choices.

### Optional but Valuable Disclosure

Beyond minimum requirements, teams should be encouraged to share:
- Comparative analyses showing changes over time (aligning with parent specification's baseline comparison guidance)
- Context about organizational constraints that affected measurement choices
- Lessons learned about what drove adoption or created barriers
- Improvement plans for advancing measurement sophistication

## 3. Threshold Criteria for Usefulness

### Minimum Accuracy Thresholds

For SCI for Web to be useful for driving the behavioral incentives identified in Section 3, it must meet minimum accuracy standards:

**For directly controlled components**: Where teams have direct control and measurement access (browsers they test with, servers they operate), accuracy should support confident decision-making. Measurements showing that implementation A has 10-15% higher energy consumption than implementation B should reliably indicate a genuine efficiency difference worth investigating.

**For modeled components with strong data backing**: Where direct measurement isn't feasible but substantial real-world data exists (network transfer, user device diversity), models should produce results within 15-20% of actual consumption. This level of accuracy is sufficient to identify major inefficiencies and track directional improvement.

**For components without adequate data**: Rather than presenting false precision, these should be explicitly marked as placeholders or rough estimates with wide uncertainty ranges, excluded from initial scope with a clear path to inclusion, or included with documented estimation methodology and clear improvement roadmap.

The key principle: measurements must be accurate enough that optimizing the measured score reliably leads to actual carbon reduction, not merely metric improvement. This prevents the "vanity metrics and proxy optimization" practice discouraged in Section 3.

### Maximum Complexity Boundaries

Complexity kills adoption. The parent SCI specification emphasizes that calculation "shall be possible without incurring any cost, for instance, for data, services, or tooling." SCI for Web should respect these boundaries:

**Parameter count**: The number of variables teams must track should be gatherable through normal development workflows. If gathering data requires dedicated data collection efforts beyond what teams already do for performance monitoring, expect resistance. This varies by organizational capability—what's feasible for a large enterprise may overwhelm a small team.

**Calculation complexity**: The calculation should be explainable to a skeptical technical manager in under five minutes. The parent SCI specification's formula `SCI = (O + M) per R` is elegant; web-specific extensions should maintain this conceptual simplicity even when operational details are more involved. If it requires specialized knowledge to understand, it will be rejected when scrutinized.

**Tool requirements**: Implementation should work with widely available, preferably open source tooling. Dependence on proprietary or expensive tools creates adoption barriers that contradict the parent specification's "easy to implement" principle and "no cost" requirement.

**Progressive entry barriers**: Teams new to sustainability measurement should be able to start with automated tooling and industry defaults. As they mature, they can invest in more sophisticated measurement. But the entry barrier must be low enough that starting is feasible for the frontend developers, backend engineers, and product managers identified in Section 2.

## 4. Gaming Prevention Principles

Section 3 identified several discouraged practices: energy displacement, quality degradation, boundary manipulation, and vanity metrics. SCI for Web must be designed to prevent these forms of gaming while avoiding paralysis through over-complexity.

### Design Against Gaming

**Measure outcomes, not proxies**: Where possible, measure actual energy consumption rather than proxy metrics that can be optimized without real impact. This aligns with the parent SCI specification's focus on quantifying actual carbon emissions (operational plus embodied) rather than indirect proxies.

**Comprehensive boundaries**: The parent specification states "The calculation of SCI shall include all supporting infrastructure and systems that significantly contribute to the software's operation." For web applications, this means measuring energy across servers, networks, third-party services, and end-user devices. Excluding major components creates displacement pathways where teams shift computation from measured to unmeasured locations without reducing total energy.

**Functional units measuring delivered value**: To discourage quality degradation, functional units should capture delivered functionality (user tasks completed, transactions processed, content consumed) rather than just technical operations (page views, API calls). This follows the parent specification's guidance that R should describe "how the application scales" in terms meaningful to its purpose.

**Avoid perverse incentives**: Ensure that optimizing for the SCI score aligns with genuine sustainability improvements. If the specification can be gamed by degrading user experience, shifting emissions elsewhere, or reducing essential quality attributes (accessibility, security, privacy), it will be gamed. Section 3 explicitly identifies these as discouraged practices.

### Balanced Perspective on Gaming Risk

Gaming is a real concern but should not cause design paralysis. Gaming requires effort, and for most teams, actually improving efficiency is easier than developing sophisticated gaming strategies. However, organizations facing performance pressure without strong sustainability culture may seek ways to show progress without actual improvement.

The solution is not paralysis through over-complexity, but transparency and clear guardrails:
- **Low-friction entry**: Make it easy to start measuring (reduces incentive to game by making genuine measurement easier than gaming)
- **Mandatory disclosure**: Make methodology, boundaries, and quantification methods visible (makes gaming detectable)
- **Clear improvement pathways**: Provide structured advancement to higher sophistication (channels competitive energy toward better measurement rather than gaming)
- **Reputational accountability**: Market scrutiny and stakeholder pressure create natural disincentives for visible gaming

### Design for Adversarial Defense

The specification must withstand scrutiny from people motivated to reject it—technical skeptics, budget guardians, and organizational resistance to sustainability investment.

**Defensible data foundation**: Every significant component should be traceable to direct measurements or well-documented datasets. Speculative models undermine credibility for the entire specification. As one participant noted, "In subjects where there are wider ethical or physical impacts, the actuality of those numbers moving is critical."

**Scope alignment with control**: Teams should only be accountable for elements they can reasonably control or influence, as defined in Section 2's persona descriptions. Measuring things beyond their control creates grounds for rejection: "Why should I be measured on something I can't affect?"

**Proportionate response to uncertainty**: Where uncertainty exists, acknowledge it rather than presenting false precision. As the parent specification acknowledges, access to data "might not always be available" and "modeling, using best estimates" is acceptable. Honest acknowledgment of uncertainty builds more trust than false precision.

## 5. Success Indicators

We will know SCI for Web succeeds when it drives the behavioral incentives identified in Section 3 and serves the target personas identified in Section 2.

### Adoption Signals

**Cross-organizational adoption**: Implementation occurs across different organizational contexts (SaaS providers, e-commerce platforms, media companies, small startups, large enterprises) without requiring extensive customization. This demonstrates that the specification serves diverse environments while maintaining consistency.

**Multi-role engagement**: The diverse roles identified in Section 2 (frontend developers, backend engineers, DevOps practitioners, product managers) can integrate SCI for Web into their workflows without specialized training for entry-level adoption.

**Sustained usage**: Teams continue measuring beyond initial implementation, indicating that the effort-to-value ratio is favorable. Measurement becomes part of normal development practice rather than a one-time compliance exercise.

**Voluntary adoption**: Organizations adopt SCI for Web before regulatory or reputational pressure makes it mandatory, suggesting genuine perceived value. This aligns with the parent specification's goal of helping "users and developers make informed choices."

**Progression over time**: Organizations advance from simpler to more sophisticated measurement approaches over time, demonstrating deepening commitment and capability.

**Industry recognition**: SCI for Web becomes the default reference in articles, conferences, and discussions about web sustainability. Industry leaders publicly adopt and advocate for the specification.

**Competitive and market pressure**: Organizations adopt SCI for Web because competitors are doing it, and not measuring becomes a competitive disadvantage. This market dynamic accelerates adoption without requiring regulatory mandates.

**Regulatory incorporation**: Government sustainability requirements and industry standards reference SCI for Web as an acceptable methodology, validating the specification's credibility.

### Impact Signals

**Behavioral change evidence**: Observable changes in development practices—optimization decisions, architectural choices, vendor selection, infrastructure planning—driven by SCI for Web insights. This is the ultimate success metric: does measurement actually change what teams build and how they build it?

**Credibility in skeptical contexts**: The specification withstands adversarial scrutiny from technically sophisticated skeptics, budget guardians, and auditors. When challenged, the measurement methodology is defensible with clear data provenance and reasonable assumptions.

**Improvement over time**: As teams iterate, their SCI scores improve, indicating that measurement is driving meaningful efficiency gains. This follows the parent specification's baseline comparison guidance: teams should be able to demonstrate that actions taken reduced their SCI score.

**Alignment with identified behavioral incentives**: The practices identified in Section 3 as encouraged (efficiency improvements, architectural optimization, responsible vendor selection, quality-preserving carbon reduction) are demonstrably incentivized by optimizing SCI for Web scores. Conversely, discouraged practices (energy displacement, quality degradation, boundary gaming) don't improve scores or are made visible through disclosure requirements.

**Prioritization capability**: Organizations use SCI for Web measurements to build Marginal Abatement Cost (MAC) curves that help prioritize sustainability investments—identifying high-impact, low-effort improvements before tackling expensive, complex optimizations. This demonstrates that the measurement framework enables practical prioritization of the three sustainability actions defined in the parent specification: energy efficiency, hardware efficiency, and carbon awareness.

**Carbon reduction at scale**: Aggregate carbon reduction across organizations implementing SCI for Web demonstrates real environmental impact. The parent specification states its purpose is "to help users and developers make informed choices... that will ultimately minimize carbon emissions." Success means actual emissions reduction, not just measurement sophistication.

**Ecosystem emergence**: Tools, services, training, and consultancies built around SCI for Web create self-sustaining momentum and reduce implementation barriers over time. This ecosystem development indicates that the specification hit the right balance between rigor and adoptability.

## 6. Implementation Feasibility Boundaries

### What We Can Reasonably Expect

The parent SCI specification acknowledges varying capabilities: "While teams should consider investing more time or money in calculating their SCI number to increase its accuracy," basic calculation "shall be possible without incurring any cost."

**Universal expectations** (feasible for all organizations):
- Automated measurement using open source tooling and reference devices for components under direct control
- Integration into CI/CD pipelines for tracking changes over time
- Documentation of methodology, boundaries, and limitations
- Measurement of directly controlled components (browser environments they test, servers they operate)

**Context-dependent expectations** (varies by organizational capability):
- Mix of direct measurement and validated modeling for broader scope
- Investment in measurement infrastructure proportional to organizational size and sustainability commitment
- Expanded scope including network transfer and third-party estimation
- Statistical validation and real-world user data integration

This recognizes that the frontend developers at small startups and the sustainability engineers at large enterprises (both identified in Section 2) have vastly different resources while both needing to adopt SCI for Web.

### What Is Too Complex to Expect Broadly

**Universal real-time monitoring**: Continuous measurement of every component creates infrastructure and complexity burdens that most teams cannot sustain. This exceeds the parent specification's "easy to implement" principle.

**Perfect accuracy across all components**: The parent specification acknowledges that "access to the data needed for higher resolution calculations might not always be available." Some components (diverse user devices, network infrastructure beyond origin servers, embodied emissions of user hardware) cannot be measured with high accuracy by most teams.

**Custom hardware instrumentation**: Expecting teams to deploy specialized measurement hardware is unrealistic for widespread adoption and contradicts the "no cost" principle.

**One-size-fits-all requirements**: Different organizational contexts face different constraints. A measurement methodology rigid enough to force uniformity will fail to achieve adoption across the diverse personas and contexts identified in Section 2.

### Third-Party Service Disclosure

Section 3 identifies third-party transparency as an encouraged practice for suppliers. Major third-party services (CDNs, analytics platforms, advertising networks, API services) should disclose carbon impact of their services. While full third-party measurement may not be feasible for most organizations, SCI for Web should create market pressure for this disclosure:

- Entry-level adoption: Document third-party services used and their handling in methodology disclosure
- Intermediate adoption: Estimate third-party impact using documented methodology (data transfer, API calls, etc.)
- Advanced adoption: Incorporate third-party disclosure data where available, use validated estimation where not

This approach balances comprehensiveness with implementation feasibility while creating market pressure for suppliers to provide transparency.

### Embodied Emissions Considerations

The parent SCI specification requires including embodied emissions: "An estimate of all the embodied emissions for the hardware used within the software boundary shall be included." For web applications, this is particularly challenging where user devices are entirely outside the application provider's control.

**Feasible approach**: Include embodied emissions for infrastructure under direct control (owned servers, owned network equipment) using the parent specification's time-share and resource-share methodology. For user devices, use documented estimation approaches based on reasonable device lifecycle assumptions and average embodied emissions data, with clear disclosure of the estimation methodology used.

This balances the parent specification's requirement with practical limitations while maintaining transparency.

## 7. Connection to Behavioral Incentives

The evaluation criteria directly enable the behavioral incentives identified in Section 3:

**Efficiency improvements made visible**: By providing accurate measurement of directly controlled components, SCI for Web makes efficiency improvements visible and attributable, creating clear incentives for the optimization practices identified in Section 3 (asset optimization, code efficiency, database optimization, infrastructure right-sizing).

**Architectural choices informed by evidence**: When architectural choices (caching strategies, rendering approaches, server/client computation distribution) show measurable impacts on SCI scores, teams gain concrete evidence to justify architectural investments identified in Section 3.

**Vendor selection enabled**: Where third-party services can be measured or compared through disclosed data, SCI for Web enables the evidence-based vendor selection identified in Section 3 as an encouraged practice.

**Quality preserved**: By measuring actual energy consumption for delivered functionality rather than crude proxies, SCI for Web rewards genuine efficiency rather than quality degradation masquerading as sustainability—explicitly preventing the discouraged practice identified in Section 3.

**Prioritization enabled**: SCI for Web enables organizations to identify high-impact, low-effort improvements through Marginal Abatement Cost curve analysis, ensuring resources are directed efficiently toward the three sustainability actions defined in the parent specification.

**Gaming prevented or exposed**: Through comprehensive boundaries and mandatory disclosure, the discouraged practices identified in Section 3 (energy displacement, boundary manipulation, vanity metrics) are either prevented by design or made visible through disclosure requirements.

## 8. Key Principles Summary

**Defensibility over comprehensiveness**: Better to measure a narrow scope accurately than claim broad coverage without credible data. Entry-level adoption measuring only directly controlled components is legitimately useful even with limited scope.

**Integration over addition**: Success requires embedding into existing workflows, not adding new exceptional processes. This serves the diverse personas identified in Section 2.

**Transparency about limitations**: False precision destroys credibility; honest acknowledgment of uncertainty builds trust. Mandatory disclosure prevents gaming and enables peer review.

**Proportionate accountability**: Hold teams accountable only for what they can reasonably control and measure, as defined in Section 2's persona descriptions. This makes rejection less likely and adoption more feasible.

**Adversarial resilience**: Design for skeptical scrutiny from technically sophisticated critics, budget guardians, and organizational resistance. Defensible data and transparent methodology withstand challenge.

**Tangible value demonstration**: Show concrete benefits—cost savings, performance improvements, competitive advantage, prioritization capability—not just sustainability scores. This aligns incentives for adoption.

**Progressive sophistication**: Enable entry at appropriate capability level while providing clear advancement pathways. All levels of sophistication are legitimate when honestly disclosed.

**Real accuracy, not perceived**: Measurements must be real because sustainability has ethical and physical implications. As one participant emphasized, "the actuality of those numbers moving is critical."

**Estimation with guardrails**: Estimation and placeholders are acceptable when clearly labeled, documented, and accompanied by improvement pathways. This follows the parent specification's allowance for modeling while maintaining transparency.

**Market pressure for improvement**: Transparency, competitive pressure, and stakeholder expectations naturally encourage sophistication advancement and third-party disclosure over time.

**Ecosystem enablement**: Lower entry barriers and clear standards enable ecosystem development (tools, services, training) that accelerates adoption and reduces future implementation costs.

**Alignment with parent SCI specification**: All evaluation criteria honor the parent specification's core characteristics (sensitivity to sustainability actions, systems-impact view, ease of implementation, encouragement of granular data) and requirements (comprehensive boundaries, disclosure, exclusion of market-based measures).

---

## Conformance to Parent SCI Specification

This evaluation criteria section aligns with the parent SCI specification's core characteristics and requirements:

**Sensitivity to sustainability actions**: The accuracy thresholds and measurement approaches are designed to be sensitive to the three sustainability actions defined in the parent specification—energy efficiency, hardware efficiency, and carbon awareness. Actions that reduce energy consumption, improve hardware utilization, or leverage lower-carbon energy will improve SCI for Web scores.

**Systems-impact view**: The emphasis on comprehensive boundaries and prevention of energy displacement ensures that SCI for Web takes the systems view required by the parent specification, preventing "local-level optimizations that might lead to negative downstream impacts."

**Easy to implement**: The progressive sophistication approach and emphasis on workflow integration honor the parent specification's requirement that "anyone without much experience or training shall be able to follow the SCI specification instructions" and that calculation be "possible without incurring any cost."

**Encouragement of granular data**: The accuracy thresholds and disclosure requirements encourage teams to use the most granular data available while allowing modeling when real-world data is unavailable, exactly as the parent specification prescribes.

**Exclusion of market-based measures**: Gaming prevention explicitly prevents using offsets, RECs, or other market-based instruments to reduce scores, following the parent specification's exclusions section.

**Disclosure requirements**: The mandatory transparency requirements extend the parent specification's procedure step 5: "Report: Disclose the SCI score, software boundary, and the calculation methodology."

The evaluation criteria ensure that SCI for Web extends the parent specification to web-specific contexts while honoring all core principles and requirements.


---

## 5. Comparative Analysis

**Purpose**: This section evaluates existing web sustainability measurement specifications and methodologies against the evaluation criteria, behavioral incentives, and target personas defined through assembly consensus. It provides evidence-based assessment of how SCI for Web compares to alternatives.

**What this section contains**:
- Overview of existing web measurement specifications and frameworks
- Structured assessment of each specification against:
  - Evaluation Criteria (Section 4) - accuracy/simplicity trade-offs, trust requirements, implementation feasibility
  - Behavioral Incentives alignment (Section 3) - does it encourage desired behaviors and prevent perverse incentives?
  - Target Personas coverage (Section 2) - does it serve the identified professional roles?
  - Parent SCI specification compatibility (Section 1) - does it align with base SCI requirements?
- Gap analysis identifying what existing approaches don't address
- Positioning of SCI for Web relative to alternatives

**What this section does NOT contain**:
- Marketing comparisons or competitive positioning
- Unsubstantiated criticism of other organizations' work
- Claims without evidence-based justification

**Methodology**:
This section IS consensus-driven. Assembly participants will evaluate existing specifications against the criteria they've already established through previous rounds. The analysis will be structured as a scoring matrix, with participants providing assessments that are then synthesized into consensus scores.

**Output format**:
Matrix showing how each existing specification scores against the established evaluation criteria, with aggregated consensus scores and identified gaps.

**Possible outcomes**:
- Confirms need for new SCI for Web specification due to identified gaps
- Identifies potential collaborations with existing initiatives
- Determines whether existing specifications could be adapted rather than creating new standard
- Clarifies unique value proposition of SCI for Web approach

**Process note**: This section will be developed through structured consensus-building after Sections 1-4 are complete. Participants will score existing specifications against the criteria they've already agreed upon, producing a comparative assessment matrix.

---

This section evaluates existing frameworks and tools against the evaluation criteria established in Section 4. The assessment aims to understand current capabilities, identify gaps, and inform the development of SCI for Web specifications.

Before presenting comparative scores, it's essential to understand what is being compared. These frameworks serve different purposes and exist at different maturity levels:

| Framework | Type | Maturity Level | Primary Purpose | Last Major Update | Links |
|-----------|------|----------------|-----------------|-------------------|-------|
| **SWDM (Sustainable Web Design Model)** | Methodology / estimation model | Mature, stable | Carbon estimation methodology for web transfers using system-wide allocation | 2024 | [SWD Methodology](https://sustainablewebdesign.org/calculating-digital-emissions/) |
| **CO2.js** | Open-source library (SWDM implementation) | Mature, stable | Programmatic implementation of SWDM for carbon estimation | 2024 (v13) | [CO2.js](https://github.com/thegreenwebfoundation/co2.js) |
| **Website Carbon Calculator** | Web application (SWDM-based) | Mature, stable | Public awareness and single-page estimation using SWDM | 2023 | [Website Carbon](https://www.websitecarbon.com/) |
| **Ecograder** | Automated testing tool (SWDM + Lighthouse) | Active development | Multi-dimensional web sustainability assessment using SWDM for carbon | 2024 (beta with WSG integration) | [Ecograder](https://ecograder.com/), [Beta](https://beta.ecograder.com/) |
| **W3C WSG** | Living standard (W3C specification) | Active development | Comprehensive sustainability guidelines for web | Ongoing (2024) | [W3C Web Sustainability Guidelines](https://w3c.github.io/sustyweb/) |
| **Parent SCI** | Technical specification (GSF standard) | Established, refinement phase | Generic software carbon intensity measurement framework | 2022 (v1.0) | [SCI Specification](https://sci.greensoftware.foundation/) |
| **Cardamon** | Web application (SCI-compatible) | Active development | SCI-compatible web carbon measurement with ground truth validation | 2024 | [Cardamon App](https://web.cardamon.io), [Paper](https://cardamon.io/sci), [Core](https://github.com/Root-Branch/cardamon-core) |
| **Green Metrics Tool** | Testing/CI platform (SCI implementation) | Mature, growing | SCI score calculation for web apps using observed hardware data | 2024 | [Green Metrics Tool](https://docs.green-coding.io), [SCI Docs](https://docs.green-coding.io/docs/measuring/carbon/sci/) |
| **Greenspector** | Testing platform | Established (France) | Carbon intensity measurement linked to functional units, CI/CD integration | 2024 | [Greenspector](https://greenspector.com/en/publicationss/) |

**IMPORTANT**: Not all frameworks listed above are independent. Several tools use the same underlying model, which is essential context for interpreting comparative scores.

The following matrices evaluate each approach against evaluation criteria from Section 4, with additional practical adoption criteria identified through community feedback.

**Scoring Scale:**
- 5: Excellent - Fully meets criteria with strong evidence
- 4: Good - Substantially meets criteria with minor gaps
- 3: Adequate - Partially meets criteria with notable limitations
- 2: Limited - Minimally addresses criteria with significant gaps
- 1: Insufficient - Does not adequately address criteria
- ~: Preliminary - Insufficient information for confident scoring

### Core Evaluation Criteria (from Section 4)

| Framework | Accuracy | Simplicity | Trust | Boundaries | Functional Units | Gaming Prevention | Personas | Incentives | **Core Avg** |
|-----------|----------|-----------|-------|------------|------------------|-------------------|----------|------------|--------------|
| **SWDM / CO2.js** | 3 | 5 | 4 | 4 | 2 | 2† | 3 | 3 | **3.3** |
| **Website Carbon Calc** | 2 | 5 | 3 | 2 | 2 | 1† | 2 | 2 | **2.4** |
| **Ecograder** | 3 | 4 | 3* | 3 | 2 | 2† | 3 | 3 | **2.9** |
| **W3C WSG** | 2* | 2 | 3 | 3 | 3 | 2 | 4‡ | 4 | **2.9** |
| **Parent SCI** | 3 | 2 | 4 | 4 | 3 | 3 | 4 | 4 | **3.4** |
| **Cardamon** | 4 | 3 | 4 | 4 | 4 | 3 | 3 | 4 | **3.6** |
| **Green Metrics Tool** | 4 | 2 | 5 | 4 | 5 | 4 | 3 | 4 | **3.9** |
| **Greenspector** | ~4 | ~3 | ~4 | ~3 | ~4 | ~3 | ~3 | ~3 | **~3.4** |

**Annotations:**
- *W3C WSG Accuracy: Acknowledged to be improving with forthcoming measurement enhancements (no release date specified). Score may increase in future assessments.
- *Ecograder Trust: Beta version now includes W3C WSG integration for improved guidance on specific improvements. Score reflects current production version capabilities.
- ‡W3C WSG Personas: Filter system exists in full document mode to sort by category/role/discipline, reducing cognitive load. Upgraded filter system planned for main documentation.
- †Gaming Prevention: Scores reduced by 1 point for SWDM-based frameworks (CO2.js, Website Carbon Calculator, Ecograder) that rely on automatic "green hosting" detection via IP/hosting provider lookup. This approach is deeply flawed for enterprise environments with CDNs and complex hosting architectures, enabling potential gaming through hosting provider selection signals rather than genuine carbon reductions.
- ~Greenspector scores are preliminary assessments based on limited publicly available documentation. Full methodology review would enable confident scoring.

**Note on SWDM-based tool scoring**: CO2.js, Website Carbon Calculator, and Ecograder share underlying SWDM methodology and therefore have similar accuracy, functional unit, and gaming prevention characteristics. Differences in other criteria reflect application-level distinctions (UI, additional features, documentation).

SCI for Web should aim to maximise its average score on the above matrix, and ensure the average score exceeds any existing entry.

---

## Next Steps

Based on this assembly report, the following actions are recommended:

1. **Participant Vote**: Present consensus positions to assembly participants for validation
2. **Project Charter Development**: If consensus is achieved, develop formal project charter for specification work
3. **Glossary Formalization**: Create GLOSSARY.md with standardized definitions
4. **FAQ Development**: Create FAQ.md addressing common questions and rationale
5. **Specification Initiation**: Begin formal SCI for Web specification development with identified scope, quality criteria, and behavioral design

---

## Acknowledgments

[Recognition of participants, facilitators, and supporting organizations]