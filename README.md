**Forked from:** https://github.com/react-csv/react-csv

# Overview :

Generate a CSV file from given data.

This data can be an array of arrays, an array of literal objects, or strings.

# Example :

```js
import { csvDownload } from "csv-download";

const csvData = [
  ["firstname", "lastname", "email"],
  ["Rana", "Shafeek", "rana@test.com"],
  ["Gayan", "Sampath", "sampath@test.com"],
  ["John", "Doe", "john@doe.com"]
];

csvDownload(csvData);
```

# Install

```
npm install csv-download --save;
```

```
yarn add csv-download;
```

# Function:

This package includes one function: 

`csvDownload(data, headers, fileName);`

## Parameters:

The function accept the following `parameters`:


### - **data (required)**:

A required property that represents the CSV data.
This data can be _array of arrays_, _array of literal objects_ or _string_.

**Example of Array of arrays**

```js
// Array of arrays. Each item is rendered as a CSV line
data = [
  ["firstname", "lastname", "email"],
  ["Rana", "Shafeek", "rana@test.com"],
  ["Sampath", "Gayana", "sampath@test.com"],
  ["Kamal", "Indika", "kamal@indika.com"]
];
```

**Example of array of literal objects**

```js
// Array of literal objects. 
// Each item is rendered as CSV line however the order of fields will be defined by the headers props. 
// If the headers props are not defined, the component will generate headers from each data item.
data = [
  { firstname: "Rana", lastname: "Shafeek", email: "rana@test.com" },
  { firstname: "Sampath", lastname: "Gayana", email: "sampath@test.com" },
  { firstname: "Kamal", lastname: "Indika", email: "kamal@indika.com" }
];
```

**Example of strings**

```js
// A string can be used if the data is already formatted correctly

data = `firstname,lastname
Rana,Shafeek
Samapth,Gayan
Kamal,Indika
`;
```

### - **headers (optional)**:

Specifying `headers` helps to define an order of the CSV fields. The csv content will be generated accordingly.

> Notes :
>
> - The meaning of headers with data of type `Array` is to order fields AND prepend those headers at the top of the CSV content.
> - The meaning of headers with data of type `String` data is only prepending those headers as the first line of the CSV content.

##### Custom Header Labels

Custom header labels can be used when converting data of type `Object` to CSV by having the header array itself be an array of literal objects of the form:

```js
{ label: /* Label to display at the top of the CSV */, key: /* Key to the data */ }
```

If the header array is an array of strings, the header labels will be the same as the keys used to index the data objects.

Example:

```js
import { csvDownload } from "csv-download";

headers = [
  { label: "First Name", key: "firstname" },
  { label: "Last Name", key: "lastname" },
  { label: "Email", key: "email" }
];

data = [
  { firstname: "Rana", lastname: "Shafeek", email: "rana@test.com" },
  { firstname: "Sampath", lastname: "Gayana", email: "sampath@test.com" },
  { firstname: "Kamal", lastname: "Indika", email: "kamal@indika.com" }
];

csvDownload(data, headers);
```

##### Nested JSON data

It is possible to reference nested strings in your data using dot notation

```js
headers = [
  { label: 'First Name', key: 'details.firstName' },
  { label: 'Last Name', key: 'details.lastName' },
  { label: 'Email', key: 'email' },
];

data = [
  { details: { firstName: 'Rana', lastName: 'Shafeek' }, email: 'rana@test.com'},
  { details: { firstName: 'Sampath', lastName: 'Gayan' }, job: 'sampath@test.com'},
];
```
Note: if at any point the nested keys passed do not exist then looks for key with dot notation in the object.

### - **fileName (optional)**:

String to specify the filename of the csv file to download.

