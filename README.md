LW Reference:
```
update ProcessData SET xpathresult = sVAR_LW_REFERENCE where xpath = "/ProcessData/Document/REFERENCE";
```
User1:
```
update ProcessData SET xpathresult = sVAR_FILENAME where xpath = "ResolveString/User1";
```
Halting:
```
update processdata set xpathresult = "false" where xpath = "/ProcessData/RouteRule/Continue";
update processdata set xpathresult = "HALTED" where xpath = "/ProcessData/Translation/Document/STATUS";
update processdata set xpathresult = "XXXXX" where xpath = "/ProcessData/Translation/Document/STATUS_REASON";
```
