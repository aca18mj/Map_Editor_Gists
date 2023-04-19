LW Reference
```pascal
update ProcessData SET xpathresult = sVAR_LW_REFERENCE where xpath = "/ProcessData/Document/REFERENCE";
```
User1
```pascal
update ProcessData SET xpathresult = sVAR_FILENAME where xpath = "ResolveString/User1";
```
Halting (LW FW)
```pascal
update processdata set xpathresult = "false" where xpath = "/ProcessData/RouteRule/Continue";
update processdata set xpathresult = "HALTED" where xpath = "/ProcessData/Translation/Document/STATUS";
update processdata set xpathresult = "XXXXX" where xpath = "/ProcessData/Translation/Document/STATUS_REASON";
```
Halting (DSV FW)
```pascal
update ProcessData set XPathResult = "IMMEDIATELY" where XPath = "ProcessData/STOP_EXECUTION";
```
Dynamic Routing
```pascal
update processdata set xpathresult = "DSV.AIRSEA" where xpath = "DynamicRoute/Route/DESTINATION_ID";
update processdata set xpathresult = "ITOXMLPDF" where xpath = "DynamicRoute/Route/DOCUMENT_TYPE";
update processdata set xpathresult = "true" WHERE xpath = "DynamicRoute/Route/Original";
```
Codelist
```pascal
select receivercode into XXXX from codelist where name = "CODELISTNAME" and sendercode = #XXXX;
```
Environment
```pascal
select xpathresult into sVAR_SYSTEM from processdata where xpath = "/ProcessData/SYSTEM";
```
Date & Time
```pascal
select xpathresult into sVAR_SYSTEM from processdata where xpath = "/ProcessData/SYSTEM"; //YYYYmmDD_HHMMSS
```
```pascal
#date << dats(5); //adds 5 days
#date >> hours(5); //removes 5 hours
```
