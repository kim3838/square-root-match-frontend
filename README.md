
# Square root match list

## Overview

This project is a web application built with Vite and Vue.

## Features

**Input Square Root Combination**: Prepend the combinations of squared value of input as C² as A² + B² = C² and Average of A,B, and C into the table

Expecting a response of

```
[
    {"value":25,"a":0,"b":5,"c":5,"avg":3},
    {"value":25,"a":3,"b":4,"c":5,"avg":4}
]
```

## Requirements

- NodeJS 20.10

## Installation

Set your api host at .env file located under the root folder, use the .env.example as a guide


```
VITE_API_ENDPOINT=http://localhost:80
```
To get started, clone the repository and install the necessary dependencies:

```
npm install
npm run dev
```

Browse the site at http://localhost:5173/