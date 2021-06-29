## Amazon QLDB JavaScript Driver

[![NPM Version](https://img.shields.io/badge/npm-v0.0.1-green)](https://www.npmjs.com/package/amazon-qldb-driver-js)
[![license](https://img.shields.io/badge/license-Apache%202.0-blue)](https://github.com/awslabs/amazon-qldb-driver-js/blob/master/LICENSE)
[![AWS Provider](https://img.shields.io/badge/provider-AWS-orange?logo=amazon-aws&color=ff9900)](https://aws.amazon.com/qldb/)

This is the JavaScript driver for Amazon Quantum Ledger Database (QLDB), which allows Web apps developers to access AmazonQLDB directly from JavaScript code running in the browser.

## Requirements

### Basic Configuration

See [Getting started in a browser script](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/getting-started-browser.html) for more information connecting to AWS.

You need to create and use an [Amazon Cognito Identity pool](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html) to provide unauthenticated access to your browser script for the Amazon QLDB service. Creating an identity pool also creates two AWS Identity and Access Management (IAM) roles, one to support users authenticated by an identity provider and the other to support unauthenticated guest users.
                                                                                                                                              

### TypeScript 3.8.x

Development of the driver requires TypeScript 3.8.x. It will be automatically installed as a dependency. It is also recommended to use TypeScript when using the driver.
Please see the link below for more detail on TypeScript 3.8.x:

* [TypeScript 3.8.x](https://www.npmjs.com/package/typescript)



## Getting Started

To use the driver, in your package that wishes to use the driver, run the following:

```npm install amazon-qldb-driver-js```

The driver also has aws-sdk, ion-js and jsbi as peer dependencies. Thus, they must also be dependencies of the package that will be using the driver as a dependency.

```npm install aws-sdk```

```npm install ion-js```

```npm install jsbi```

Then from within your package, you can now use the driver by importing it. This example shows usage in TypeScript specifying the QLDB ledger name and a specific region:

```javascript
const { CognitoIdentityClient } = require("@aws-sdk/client-cognito-identity");
import { QldbDriver } from "amazon-qldb-driver-js";

const testServiceConfigOptions = {
    region: "us-east-1",
    credentials: fromCognitoIdentityPool({
        client: new CognitoIdentityClient({ region: "us-east-1" }),
        identityPoolId: "IDENTITY_POOL_ID" // IDENTITY_POOL_ID
  }),
};

const qldbDriver: QldbDriver = new QldbDriver("testLedger", testServiceConfigOptions);
qldbDriver.getTableNames().then(function(tableNames: string[]) {
    console.log(tableNames);
});
```

### See Also

1. QLDB JavaScript driver accepts and returns [Amazon ION](http://amzn.github.io/ion-docs/) Documents. Amazon Ion is a richly-typed, self-describing, hierarchical data serialization format offering interchangeable binary and text representations. For more information read the [ION docs](http://amzn.github.io/ion-docs/docs.html).
1. [Amazon ION Cookbook](http://amzn.github.io/ion-docs/guides/cookbook.html): This cookbook provides code samples for some simple Amazon Ion use cases.
1. Amazon QLDB supports the [PartiQL](https://partiql.org/) query language. PartiQL provides SQL-compatible query access across multiple data stores containing structured data, semistructured data, and nested data. For more information read the [PartiQL docs](https://partiql.org/docs.html).
1. Refer the section [Common Errors while using the Amazon QLDB Drivers](https://docs.aws.amazon.com/qldb/latest/developerguide/driver-errors.html) which describes runtime errors that can be thrown by the Amazon QLDB Driver when calling the qldb-session APIs.

## Development

### Setup

To install the dependencies for the driver, run the following in the root directory of the project:

```npm install```

To build the driver, transpiling the TypeScript source code to JavaScript, run the following in the root directory:

```npm run build```

### Running Tests

You can run the unit tests with this command:

```npm test```

or

```npm run testWithCoverage```

### Integration Tests

You can run the integration tests with this command:

```npm run integrationTest```

This command requires that credentials are pre-configured and it has the required permissions.

Additionally, a region can be specified in: `src/integrationtest/.mocharc.json`.

### Documentation 

TypeDoc is used for documentation. You can generate HTML locally with the following:

```npm run doc```

## License

This project is licensed under the Apache-2.0 License.

