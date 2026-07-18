# BatchConfig

Configuring for [Resequence EIP](resequence-eip.md) in batching mode.

The BatchConfig eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **batchSize** | Sets the size of the batch to be re-ordered. The default size is 100. | 100 | Integer |
| **batchTimeout** | Sets the timeout for collecting elements to be re-ordered. The default timeout is 1000 msec. | 1000 | String |
| **allowDuplicates** | Whether to allow duplicates. | false | Boolean |
| **reverse** | Whether to reverse the ordering. | false | Boolean |
| **ignoreInvalidExchanges** | Whether to ignore invalid exchanges. | false | Boolean |

## Exchange properties

The BatchConfig eip has no exchange properties.