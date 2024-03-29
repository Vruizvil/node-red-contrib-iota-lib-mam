# Node-red IOTA MAM module

This is fork from https://www.npmjs.com/package/node-red-contrib-iota-mam
Original Release 4.1.2 https://gitlab.com/ouya/node-red-contrib-iota-mam.git

## Requirements

Install node-red globally and install ui packages

```
sudo npm install -g --unsafe-perm node-red
```

in your ~/.node-red installation directory type:
```
npm install node-red-dashboard

```

# IOTA-MAM module installation

Run the following command in your NODE-RED install
```
npm install node-red-contrib-iota-lib-mam
```

# Usage

Two different function nodes are now available for

**MAM publish** (=upload data to tangle)
and
**MAM fetch** (=download data from tangle)

Drag MAM function node into a flow and wire it accordingly

If you have any issues regarding this module, please test with this file and give a clear issue description. Thank you!

## MAM fetch

Start deploying a single 'mamFetch function node'.
Set its root property (**root = "your MAM_ROOT"**)

wire this node's output to
-> any output ( e.g. a chart displaying your msg.payload)

> try with NHNRYMKA9RLTPLQNWFRHKJGVUXAAPBVYBG9LOXFPKDWVKOUIDILEVCBNGLOPYZEGZMEFSCOOVCKNOPSNB)

This should hold a non-encrypted (public) data packet sequence. (as of 18 april 2019)


## MAM publish

wire its output to
-> mamPublish node

and wire this node's output to an
-> (optional) output for logging

The MAM publish now operates in a loop:

1)  collects input data from sensorTag (can be a mix of temperature, lux etc)
2)  and immediately uploads the 1st data packet to the tangle

loop:
  ... now waiting for the bundle and its transactions to be confirmed on the tangle, it aggregates all incoming sensor tag data into a data array ...
  upon MAM confirmation of the previous bundle, it sends this aggregated data array to the tangle
  ... now waiting again for bundle confirmation

### Rate limits
on many public nodes you might have rate limits, so better use your own custom node, or make sure the node you connect to has the capacity to handle your sensor data traffic.
