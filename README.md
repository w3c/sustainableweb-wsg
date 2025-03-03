# Web Sustainability Guidelines (WSG)
Welcome to the repository of the [Web Sustainability Guidelines (WSG)](https://w3c.github.io/sustainableweb-wsg/).

If you would like to learn more about us and how to participate in this project, please check the readme in the [W3C Sustainable Web Interest Group](https://github.com/w3c/sustainableweb-ig) repository.

## Statistics

 - **94** Guidelines covering UX, Web Development, DevOps, & Business / Product Strategy.
 - **255** Success Criteria to meet the guidelines on various aspects of sustainability.
 - **100+** contributors from over **20** nations around the world.

## Work

The chartered focus of the [W3C Sustainable Web Interest Group](https://www.w3.org/groups/ig/sustainableweb/) is the development of the Web Sustainability Guidelines (WSG) and its deliverables.

Links to relevant documents (based on the CG Draft Report) can be found below.

**Guidelines:**
<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Status</th>
			<th>Date</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/">Web Sustainability Guidelines</a> (WSG)</td>
			<td>W3C Editors Draft</td>
			<td>17 Feb 2025</td>
		</tr>
	</tbody>
</table>

**Other Deliverables:**
<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Status</th>
			<th>Date</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/star.html">Sustainable Tooling And Reporting</a> (STAR)</td>
			<td>W3C Editors Draft</td>
			<td>17 Feb 2025</td>
		</tr>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/glance.html">WSG At A Glance</a></td>
			<td>W3C Editors Draft</td>
			<td>14 Feb 2025</td>
		</tr>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/intro.html">Introduction to Web Sustainability</a></td>
			<td>W3C Editors Draft</td>
			<td>10 Feb 2025</td>
		</tr>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/policies.html">Web Sustainability Laws & Policies</a></td>
			<td>W3C Editors Draft</td>
			<td>12 Feb 2025</td>
		</tr>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/quickref.html">Quick Reference for WSG</a> & <a href="https://w3c.github.io/sustainableweb-wsg/checklist.pdf">Checklist</a> (PDF)</td>
			<td>W3C Editors Draft</td>
			<td>17 Feb 2025</td>
		</tr>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/guidelines.json">WSG JSON API</a></td>
			<td>JSON API</td>
			<td>17 Feb 2025</td>
		</tr>
		<tr>
			<td><a href="https://w3c.github.io/sustainableweb-wsg/star.json">STAR JSON API</a></td>
			<td>JSON API</td>
			<td>19 Feb 2025</td>
		</tr>
		<tr>
			<td><a href="https://github.com/w3c/sustainableweb-wsg/tree/main/test-suite">STAR Test Suite</a></td>
			<td>Test Suite</td>
			<td>17 Feb 2025</td>
		</tr>
	</tbody>
</table>

## Schedule
<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Date</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Initial Draft</td>
			<td>30 June 2025</td>
		</tr>
		<tr>
			<td>Final Draft</td>
			<td>31 December 2025</td>
		</tr>
		<tr>
			<td>Measurability</td>
			<td>31 Mar 2026</td>
		</tr>
		<tr>
			<td>W3C Draft Note</td>
			<td>22 Apr 2026 (<i>Earth Day</i>)</td>
		</tr>
		<!--
		<tr>
			<td>Horizontal Review</td>
			<td>TBD</td>
		</tr>
		<tr>
			<td>W3C Note</td>
			<td>TBD</td>
		</tr>
		<tr>
			<td>W3C Statement</td>
			<td>TBD</td>
		</tr>
		-->
	</tbody>
</table>

**Note:** We will still consider the [remaining proposed and planned updates](https://docs.google.com/presentation/d/1dcuSMLcAF8jTHNCovOfs31zrjCr3rtrwzTXRLSy3lAk/edit?usp=sharing) carried forward from the Sustainable Web Community Group (based on both W3C and CG member feedback).

## Processes

Work is planned in accordance with the [issues](https://github.com/w3c/sustainableweb-wsg/issues) requiring resolution.

If you would like to contribute towards this specification, please refer to the [CONTRIBUTING.md](IG-CONTRIBUTING.md) document for details and refer to the guidance on the [W3C Sustainable Web Interest Group](https://github.com/w3c/sustainableweb-ig) repository readme regarding participation.

## JSON APIs

We have two JSON APIs which are kept in sync with the changes occurring within our [specification](https://w3c.github.io/sustainableweb-wsg/guidelines.json) and [STAR](https://w3c.github.io/sustainableweb-wsg/star.json).

These documents are reachable via GitHub pages and can be queried using JavaScript to embed our data within your client of choice.

**WSG** (*guidelines.json*)
```
category[1].guidelines[0].guideline = "Display any variables that have a negative impact on your project"
```
**STAR** (*star.json*)
```
category[1].techniques[0].title = "Produce a List of Variables To Monitor for Sustainability Impacts"
```

**Note:** To match a WSG guideline to a STAR technique, you can match the guideline `testable` anchor hash (WSG JSON API) to the technique `id` (STAR JSON API).

## Test Suite

We have a [Test Suite](https://github.com/w3c/sustainableweb-wsg/tree/main/test-suite) which is used to showcase machine testability (as denoted in [STAR](https://w3c.github.io/sustainableweb-wsg/star.html)) for the Web Sustainability Guidelines (WSGs). The template structure for the file uses common W3C conventions for test cases to maintain interoperability for tooling that wishes to align our work with their own.

Key concepts of note include:
- Each title element contains a short identifier for the test.
- The rel="author" link element contains details of who created that test.
- The rel="help" link element links to the WSG guideline it relates to.
- The name="flags" meta element identifies any requirements the test may have such as an external file (**asset**), scripting (**JavaScript**), user-involvement (**interaction**), or if it's trying to disprove something (**invalid**).
- The name="assert" meta tag explains which **STAR** technique it relates to by title.
- The conditions of passing are what requirements are necessary to pass the technique (and thus the success criteria).

## Resources

Below are some handy links for contributors to our project:

 - [Charter Template](https://w3c.github.io/charter-drafts/charter-template.html) ([HTML Source](https://github.com/w3c/charter-drafts/blob/gh-pages/charter-template.html))
 - [GRI Notebook](GRI.ipynb) ([Spreadsheet](https://docs.google.com/spreadsheets/d/12nGydnSv24fvmvCM-665_pFGPG9u3RgTwe1sCz4eiGk/edit?usp=sharing))
 - [How to do Wide Review](https://www.w3.org/Guide/documentreview/)
 - [Policies & legal information](https://www.w3.org/policies/)
 - [Pubrules documentation](https://www.w3.org/pubrules/doc/)
 - [QA Framework](https://www.w3.org/TR/qaframe-spec/)
 - [Repository Templates](https://github.com/w3c/ash-nazg/tree/master/templates)
 - [ReSpec Documentation](https://respec.org/docs/)
 - [STAR Testability](https://docs.google.com/spreadsheets/d/1DKfIdm0mHkyzTVv41hogUdh41SnLkk9Uwkc8Nm6bqD4/edit?usp=sharing)
 - [TAG Explainers](https://tag.w3.org/explainers/)
 - [Title Case Converter](https://titlecaseconverter.com/)
 - [The Art of Consensus](https://www.w3.org/Guide/)
 - [W3C Manual of Style](https://www.w3.org/Guide/manual-of-style/)
 - [W3C Process for Busy People](https://github.com/w3c/wg-effectiveness/blob/main/process.md)
