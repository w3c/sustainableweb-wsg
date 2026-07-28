# Web Sustainability Guidelines (WSG)
Welcome to the repository of the [Web Sustainability Guidelines (WSG)](https://www.w3.org/TR/web-sustainability-guidelines/).

If you would like to learn more about us and how to participate in this project, please check the readme in the [W3C Sustainable Web Interest Group](https://github.com/w3c/sustainableweb-ig) repository.

## Processes

Work is planned in accordance with the [issues](https://github.com/w3c/sustainableweb-wsg/issues) requiring resolution.

If you would like to contribute towards this specification, please refer to the [CONTRIBUTING.md](CONTRIBUTING.md) document for details and refer to the guidance on the [W3C Sustainable Web Interest Group](https://github.com/w3c/sustainableweb-ig) repository readme regarding participation.

## JSON API

We have a JSON API which is kept in sync with the changes occurring within our [specification](https://w3c.github.io/sustainableweb-wsg/guidelines.json).

This document is reachable via GitHub pages and can be queried using JavaScript to embed our data within your client of choice.

**WSG** (*guidelines.json*)
```js
category[1].guidelines[0].guideline = "Identify, assess, disclose, review, and mitigate sustainability impacts"
```

One method of reaching the API could be through code similar to the below (customize to your requirements):

```js
fetch("https://w3c.github.io/sustainableweb-wsg/guidelines.json")
  .then((res) => res.json())
  .then((data) => {
    console.log(`The First UX Guideline Title is ${data.category[1].guidelines[0].guideline}`); });
```