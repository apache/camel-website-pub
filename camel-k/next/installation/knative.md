# Knative configuration

"[Knative](https://knative.dev) is an Open-Source Enterprise-level solution to build Serverless and Event Driven Applications". The effort done in this project is a great complement to Camel K, which can leverage some feature offered by Knative. In particular, Camel K will be able to leverage "scale to 0" (hence, serverless) feature offered by Knative.

> **Note**
> Knative is an optional configuration. It is not required to run Camel K.

## Knative privileges

Camel K needs to have certain privileges to use the resources used by Knative. However, the installation procedure should take care of all the privileges aspects regardless the installation methodology you’re using.

> **Note**
> you should [install Knative](https://knative.dev/docs/install/) "Serving" resources before installing and running Camel K Operator. This is required because the operator "watches" certain resources installed by Knative. If yuo install Knative after Camel K, then, you must restart Camel K operator Pod in order to watch the Knative resources accordingly.

From now on you should be able to run some Camel application leveraging Knative with Camel K (see [examples](https://github.com/apache/camel-k-examples/tree/main/generic-examples/knative)).