# StreamConfig

Configuring for [Resequence EIP](resequence-eip.md) in stream mode.

The StreamConfig eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **capacity** | Sets the capacity of the resequencer inbound queue. | 1000 | Integer |
| **timeout** | Sets the minimum time (milliseconds) to wait for missing elements (messages). | 1000 | String |
| **deliveryAttemptInterval** | Sets the interval in milliseconds the stream resequencer will at most wait while waiting for the condition of being able to deliver. | 1000 | String |
| **ignoreInvalidExchanges** | Whether to ignore invalid exchanges. | false | Boolean |
| **rejectOld** | If true, throws an exception when messages older than the last delivered message are processed. | false | Boolean |
| **comparator** | To use a custom comparator for ordering the sequence of messages. |  | ExpressionResultComparator |

## Exchange properties

The StreamConfig eip has no exchange properties.