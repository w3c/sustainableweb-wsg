# SCI for Web Specification \-- Expert Assembly Programme

**Purpose**: 

This document reflects Harmony's architecture as of February 2026\.  
This document defines a sequential programme for an assembled group of experts to refine SPEC-draft-v2.md into a final SCI for Web specification. Sessions are ordered by dependency: foundational decisions first, validation and sign-off last.

---

## Decision Model

Each session should ultimately aim for consensus using the ENDORSE / CONSENT / OBJECT model used in the REPORT.md assembly process. Use Harmony DISCOVER and DELIBERATE phases to refine the content and navigate compromises and trade-offs such that what is presented for voting is highly likely to pass without objections. Where consensus cannot be reached, dissenting positions should be documented alongside the majority position.

## Pre-Reading

All participants should read before Session 1:

- REPORT.md (design requirements)  
- SPEC.md (the draft under review)  
- Parent SCI Specification (ISO/IEC 21031:2024)  
- Harmony primers

---

## Programme

### Session 1: Formula Structure and Functional Units

**Draft reference**: Sections 5, 6.4, 7, 8.1

**Purpose**: Establish the complete architecture of the SCI equation \-- the six components in the numerator and the functional unit in the denominator. Every subsequent session depends on these being correctly defined.

**Part A \-- Formula Validation**:

1. **Are the six components correct and complete?** Is there a component missing (e.g., `M_network` for embodied emissions of network infrastructure)? Is any component unnecessary or redundant?  
2. **Are the boundaries between components clear enough to prevent double-counting?** Specifically: where does O\_server end and O\_network begin for CDN edge servers? Where does O\_client end and O\_thirdparty begin for third-party scripts executing in the browser?  
3. **Is the SWDM double-counting guidance sufficient?** SWDM allocates energy across datacenter, network, and end-user segments. The draft says to use only the network segment for O\_network. Is this workable?  
4. **Should M\_network be included or explicitly excluded?** Network infrastructure has embodied emissions. Is the current implicit exclusion appropriate?

**Part B \-- Functional Units**:

5. **Are the recommended functional units per application type practical?** Can practitioners actually measure "content items consumed" or "tasks completed" with existing analytics tooling?  
6. **Are the discouraged functional units correctly identified?** Are there cases where "page views" or "API calls" are genuinely the right choice?  
7. **How should engagement thresholds be defined?** For "user session" \-- what constitutes a qualifying session? Mandate minimum thresholds or leave to organizations?  
8. **What about multi-purpose applications?** Should different functional units apply to different sections, or must there be a single R?  
9. **How do functional units handle bot traffic and non-human access?** Exclude from R, include, or handle differently?

**Expected output**: Validated component list and boundary definitions. Refined functional unit guidance with practical measurement examples.

---

### Session 2: Server-Side and Network Measurement

**Draft reference**: Sections 8.2, 8.3, 8.6

**Dependency**: Session 1

**Purpose**: Define the measurement methodology for components under infrastructure team control \-- server-side operational emissions (O\_server), network transfer emissions (O\_network), and server-side embodied emissions (M\_server). These are the best-understood components and form the measurement baseline.

**Questions \-- Server-Side (O\_server, M\_server)**:

1. **Is the PUE-based calculation sufficient for datacenter energy?** Should the specification provide default PUE values by provider type (hyperscale cloud, colocation, on-premise)?  
2. **How should serverless and edge computing energy be attributed?** Cold starts, shared infrastructure, per-invocation billing \-- what allocation methodology is defensible?  
3. **How should multi-tenant cloud infrastructure be attributed?** vCPU-based, memory-based, or cost-based allocation? What do cloud carbon tools actually provide?  
4. **Are the M\_server calculation methods practical?** Can teams using cloud infrastructure actually obtain embodied emissions data? Which databases (Boavizta, CCF) are reliable?

**Questions \-- Network (O\_network)**:

5. **Is SWDM v4 the right default model?** What are its known limitations? Are the coefficients appropriate?  
6. **Should the specification provide its own network energy coefficients?** If SWDM is insufficient, what alternatives exist?  
7. **How should WiFi vs. cellular vs. wired be handled?** Require differentiation or accept a blended average?  
8. **How should caching reduce O\_network?** If a returning user loads 80% from browser cache, should O\_network be 80% lower? How is this measured?  
9. **What carbon intensity should be used for network infrastructure?** Is a global average the only practical option?

**Expected output**: Validated server-side and network measurement methodology with recommended defaults and coefficients.

---

### Session 3: Client-Side Measurement

**Draft reference**: Sections 8.4, 16

**Dependency**: Session 1

**Purpose**: Client-side measurement is the most novel and uncertain aspect of SCI for Web. This is where the REPORT.md identified the greatest tension between accuracy and feasibility. It warrants a dedicated session.

**Questions**:

1. **What tools and methods actually work for client-side energy measurement?** Browser DevTools give CPU/GPU time but not energy in kWh. What conversion factors or proxy models are defensible? What is the state of the art?  
2. **How should the reference device list be maintained?** Name specific models updated annually, or maintain device classes and let organizations choose?  
3. **Is the three-tier approach (reference device / device mix / RUM) correct?** Is RUM actually feasible for energy measurement with current browser APIs? What APIs exist or are emerging?  
4. **How should screen energy be handled?** A significant portion of device energy during browsing is the display. Include in O\_client? If so, how?  
5. **What default conversion factors should be provided?** If a team measures CPU time in milliseconds on a reference device, what factor converts to kWh? What research supports these factors?  
6. **How should idle vs. active energy be attributed?** When a browser tab is open but the user isn't interacting, should baseline energy draw be attributed to the web application?

**Expected output**: Validated client-side measurement methodology with specific tool recommendations, conversion factors, and handling of screen energy.

---

### Session 4: Third-Party Services, Embodied Emissions, and Default Values

**Draft reference**: Sections 5.4, 8.5, 8.7

**Dependency**: Sessions 1-3

**Purpose**: Addresses the two areas where practitioners must rely most heavily on external data and estimation: third-party service emissions and embodied emissions from end-user devices. Both require the assembly to agree on defensible default values where direct measurement is impractical. Grouping them ensures consistent treatment of uncertainty and disclosure.

**Questions \-- Third-Party Services (O\_thirdparty)**:

1. **Are the three estimation methods (vendor disclosure, API call estimation, data transfer estimation) sufficient?** Are there other practical approaches?  
2. **What default energy-per-API-call values are defensible?** The predraft suggested 0.0001 kWh per API call. Reasonable? For which service types?  
3. **Should there be a mandatory minimum list of third-party services?** e.g., "Analytics, advertising, and payment processing SHALL always be included if present." Or is the 1% materiality threshold sufficient?  
4. **How should client-side third-party scripts be attributed?** A GA script executes on the user's device (O\_client) and sends data to Google's servers (O\_thirdparty). Where does the energy go?  
5. **What is realistic to expect from vendors?** Which vendors currently provide energy/carbon data? Is there a pathway to standardized vendor disclosure?  
6. **How should advertising networks be handled?** Ad auctions, real-time bidding, and dynamic creative consume energy across multiple parties. Is there a practical approach?

**Questions \-- Embodied Emissions (M\_client)**:

7. **Are the default embodied emissions values correct?** What LCA databases support 400 kg for desktops, 300 kg for laptops, 100 kg for tablets, 80 kg for smartphones?  
8. **Are the default lifespans correct?** 5 years for desktops, 4 years for laptops, 3 years for smartphones \-- do these match real-world replacement cycles?  
9. **How should the default device mix distribution be determined?** The predraft suggested 30% desktop, 20% laptop, 40% smartphone, 10% tablet. What data supports this?  
10. **How should resource-share work for client devices?** CPU utilization as a proxy \-- sufficient, or should GPU, memory, and display be considered?  
11. **Should M\_client include peripherals?** External monitors, keyboards, chargers \-- include or exclude?  
12. **How frequently should default values be updated?** Should the specification commit to an update cadence?

**Expected output**: Refined third-party measurement methodology with default values. Validated embodied emissions defaults with cited sources. Governance process for maintaining default values over time.

---

### Session 5: Implementation Tiers, Tooling, and Disclosure

**Draft reference**: Sections 9, 12, Appendix A

**Dependency**: Sessions 1-4

**Purpose**: With measurement methodology settled, this session defines how organizations adopt SCI for Web (tiers and tooling) and how they report results (disclosure). These are two sides of the same coin \-- tiers determine what you measure, disclosure determines what you report.

**Questions \-- Implementation Tiers**:

1. **Are the tier boundaries correct?** Is the jump from Entry to Standard too large? Is there a gap where many organizations would fall between tiers?  
2. **Are Entry tier requirements achievable at zero cost?** The parent SCI specification says calculation "shall be possible without incurring any cost." Can a small team actually complete an Entry tier calculation?  
3. **Should there be a "Starter" tier below Entry?** e.g., measuring only O\_server and O\_network with defaults for everything else?  
4. **What specific tools satisfy each tier?** Name open-source tools for Entry tier today. Standard tier. Where are the gaps?  
5. **How should tier advancement be incentivized?** Recommended timeline, or purely voluntary?  
6. **Should the specification mandate minimum tiers for specific contexts?** Large organizations, public sector, or those making public sustainability claims?

**Questions \-- Disclosure**:

7. **What structured format should the disclosure template use?** JSON, YAML, JSON-LD? Align with existing sustainability reporting formats?  
8. **What is the minimum viable disclosure?** The mandatory list has 10 items. Too many for Entry tier? Too few for credibility?  
9. **Should there be a standardized badge or label format?** e.g., "SCI for Web: 7.96 gCO2eq/transaction \[Standard Tier\]" \-- embeddable on a website?  
10. **How should disclosures be versioned and archived?** Should previous disclosures remain accessible?  
11. **Should there be a registry of published SCI for Web scores?** This would enable industry benchmarking.

**Expected output**: Validated tier definitions with tooling examples. Draft disclosure template with mandatory and optional fields.

---

### Session 6: Worked Examples, Reference Values, and Edge Cases

**Draft reference**: Sections 11, 13, Appendices B-D

**Dependency**: Sessions 1-5

**Purpose**: Validate the specification end-to-end by working through complete calculations for realistic scenarios, and stress-test it against the diversity of real web architectures. This is where theory meets practice.

**Questions \-- Worked Examples and Reference Values**:

1. **Do the example calculations produce realistic numbers?** Are 7.96 g CO2eq per e-commerce transaction, 0.63 g per article read, and 30.7 g per SaaS session in the right order of magnitude?  
2. **Can we produce a complete worked example with real data?** Walk through the full calculation for a real (or realistic) web application, identifying every data point, assumption, and estimation.  
3. **What reference coefficients should Appendix C contain?** Compile the specific numbers: PUE defaults, network energy per GB, kWh-per-API-call defaults, carbon intensity global averages, etc.  
4. **What tools should Appendix D recommend?** For each component and tier, which specific tools? Where are gaps?  
5. **How do the examples validate against existing tools?** If we calculate a score and also measure with Green Metrics Tool or Cardamon, do results broadly agree?

**Questions \-- Edge Cases and Architectural Patterns**:

6. **Static sites with heavy client-side interactivity** (Jamstack \+ SPA hybrid): Where does SSG end and SPA begin? How should build-time vs. runtime be handled?  
7. **Streaming media platforms**: Video/audio streaming is bandwidth-intensive. How should continuous media delivery be measured?  
8. **Real-time collaborative applications**: WebSocket-heavy apps with persistent connections. How should always-on connections be attributed?  
9. **Multi-tenant SaaS**: How should a single platform serving thousands of customers allocate emissions per customer?  
10. **Micro-frontend architectures**: Multiple independently deployed frontends composed in the browser. Who owns the SCI score?  
11. **Offline-first PWAs**: How should applications that sync periodically be measured?  
12. **Multi-region CDN deployments**: Same content served from dozens of edge locations. How should I\_server be calculated?

**Expected output**: Validated examples, populated appendices (reference values and tool directory), expanded edge case guidance.

---

### Session 7: Gaming Prevention and Adversarial Review

**Draft reference**: Sections 7.4, 17, 18; REPORT.md Section 3 (Discouraged Practices)

**Dependency**: Sessions 1-6

**Purpose**: With the specification substantially complete, the assembly attempts to game it. Participants actively try to find ways to reduce scores without genuinely reducing emissions. This is an adversarial review, not a cooperative one.

**Attack vectors to test**:

1. **Energy displacement**: Can a team shift computation from O\_server to O\_client (or vice versa) to reduce their total SCI score? Does the comprehensive boundary prevent this?  
2. **Boundary manipulation**: Can a team exclude high-emission components through creative boundary definition? Does the mandatory inclusion list prevent this?  
3. **Functional unit gaming**: Can a team choose a functional unit that makes their inefficient application appear efficient?  
4. **Third-party externalization**: Can a team outsource computation to third-party services to move emissions from O\_server to O\_thirdparty, then exclude them under the 1% materiality threshold?  
5. **Quality degradation**: Can a team reduce page weight by degrading quality (low-res images, removed features) and show a lower SCI score?  
6. **Tier shopping**: Can a team choose Entry tier specifically to avoid measuring components where they perform poorly?  
7. **Measurement period cherry-picking**: Can a team select an atypical low-traffic period to improve their per-R score?

For each vulnerability found, the assembly should either:

- **Amend the specification** to close the vulnerability, or  
- **Document it as a known limitation** where gaming cannot be fully prevented but is made detectable through disclosure requirements

**Expected output**: Identified vulnerabilities with specification amendments. Documented known limitations.

---

### Session 8: Final Review and Sign-Off

**Dependency**: Session 8

**Purpose**: Final consensus session on the release candidate. The assembly formally endorses (or objects to) the specification for release to public comment.

**Agenda**:

1. Presentation of the release candidate (section-by-section summary)  
2. Final ENDORSE / CONSENT / OBJECT round on the complete specification  
3. Document any remaining objections or minority positions  
4. Agree on post-assembly process:  
   - Public comment period duration and mechanism  
   - Pilot implementation candidates (aim for 3-5 organizations)  
   - Governance for future specification updates and default value maintenance  
   - Timeline to Version 1.0 publication  
5. Close the assembly

**Expected output**: Endorsed release candidate ready for public comment. Documented post-assembly governance.

---

## Post-Assembly Process

After Session 8 sign-off:

1. **Public comment period** (30 days): Open the release candidate for broader community review  
2. **Comment resolution** (2 weeks): Address public comments, produce final specification  
3. **Pilot implementation** (8-12 weeks): 3-5 organizations implement the specification and provide feedback  
4. **Version 1.0 publication**: Final specification incorporating pilot feedback

---
