# Eddystone-EURL

Eddystone-EURL is an implementation of the Eddystone-URL frame with an added ephemeral identifier from the Eddystone-EID frame. It the  broadcasts a URL with a single query string parameter representing the EID.

This combination suppliments the universal access Physical Web philosophy of Eddystone-URL with a "proof of location" (proximity to beacon) assurance from Eddystone-EID. It allows Physical Web services to be limited only to users who have been genuinely physically near a beacon within a set time period, without the need for bespoke clients or apps. It is designed to prevent abuse of otherwise gloablly web-accessible services.

As with Eddystone-URL, the URL can be used by any client with access to the internet.  For example, if an Eddystone-EURL beacon were to broadcast the URL `http://bit.do/bVVjk?6qpJ`, then any client that received this packet could choose to [visit that url](http://bit.do/bVVjk?6qpJ). The difference is the inclusion of an ephemeral identifier on the URL which the resulting websever can act on.

This puts the power in the hands of the website owner, who can choose whether or not to validate the EID, decide on what time range is acceptable, and what to do on success or failure. It allows Physical Web services to provide a level of guarantee that the user is or has recently been genuinely physically co-located with the beacon.
Example use cases:
* A coffee shop provides its daily WiFi password on a webpage only to those who have visited the shop that day
* A restaurant allows customers to place their order online, but only from within the restaurant
* A Jukebox provides a Physical Web interface, only to customers currently nearby

Note that URL shorteners are highly recommended when using Eddystone-EURL, however not all URL shortening services passthrough query parameters.

## URL Structure

|Field  | Example
|:------- | :---------
| URL   					  | `http://bit.do/bVVjk`
| Query string begin| `?`
| Encoded EID       | `6qpJ`

The resulting URL would be `http://bit.do/bVVjk?6qpJ`.

The EID is base64 encoded and appended to the URL up to the maximum number of character allowed by the Eddystone-URL frame (18). 

The [eidtools.py](tools/eidtools.py) utility may be of use in testing implementations of EURL beacons.

## Security

The length of the EID affects the level of assurance it provides; a longer EID is less vulnerable to being forged within the valid timeframe.

The encoded EID length can be maximised by limiting the length of the base URL, thus the security level is left to the choice of the owner. Shorter encoded EIDs should be mitigated by more frequent EID rotation periods.

## See Also

* **[Eddystone-URL](../eddystone-url/README.md)** — Eddystone URL specification
* **[Eddystone-EID](../eddystone-eid/README.md)** — Eddystone EID specification