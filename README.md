# Cribl Inline Reduction Report

This pipeline is intended to be used with another pipeline to batch test a large archive of logs. The built-in preview/sample interface cannot handle files that are hundreds of MB or more. This can replicate some of that functionality with arbitrarily large sample files.

## Recommended steps to use

1) Create a Collector source pointing to an NFS share or object store with your sample file
  * Alternatively, you can use a raw TCP source, and feed the file to the port using `netcat`
2) Be sure you have an Event Breaker assigned to the source that works for your test data
4) Add this Pipeline to your Worker Group
5) Change the Chain function to point to the Pipeline or Pack you want to test
6) Under Routing, Quick Connect, connect your source to the devnull destination, and select the cribl_inline_redux_report Pipeline
  * Optionally deliver to your analytics tool
7) Navigate back to the source page and prepare to make a Full Run on your collector
  * Or prepare to fire off `netcat` with your file
9) In a new window or tab, start a capture with your source as the filter
  * To help with the capture filter, you might add a field to the Collector definition, eg `_TEST_FIELD` => `1`, and filter on that
11) With the capture running, go back to the tab with the Collector source and run it (or fire off your `netcat`)
12) The capture should show you 2 events: 1 for the original stats, and 1 for the processed stats

