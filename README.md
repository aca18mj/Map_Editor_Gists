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
DB Connection
```pascal
object oVAR_CONNECTOR;
string[512] sVAR_TMP_SQL;
string[256] sVAR_CTRL_NUM;
integer iVAR_CTRL_NUM;
sVAR_TMP_SQL = "";
sVAR_CTRL_NUM = "";
iVAR_CTRL_NUM = 0;
oVAR_CONNECTOR = new("com.stercomm.emea.mstrombrink.dbpoolconnector.Connector");
oVAR_CONNECTOR.debugInfoMapName("YOUR_MAP_NAME");
oVAR_CONNECTOR.doDebug();
oVAR_CONNECTOR.connect("DSV_PARTNER_EDI_CONF");
oVAR_CONNECTOR.transactionStart();
sVAR_TMP_SQL = "SELECT CONTROL_NUMBER_VALUE FROM DSV_ControlNumber_tb WHERE CONTROL_NUMBER_NAME= 'DSV_XXXXX_RECADV_ctl' FOR UPDATE WITH RR";
iVAR_CTRL_NUM = oVAR_CONNECTOR.getResultAsIntegerExistingConn(sVAR_TMP_SQL, "CONTROL_NUMBER_VALUE");
if iVAR_CTRL_NUM >= 2147483647 then
   iVAR_CTRL_NUM = 1;
    
iVAR_CTRL_NUM = iVAR_CTRL_NUM + 1;
ntoa(iVAR_CTRL_NUM, sVAR_CTRL_NUM);
sVAR_TMP_SQL = "UPDATE DSV_ControlNumber_tb SET CONTROL_NUMBER_VALUE = " + sVAR_CTRL_NUM + " WHERE CONTROL_NUMBER_NAME= 'DSV_XXXX_RECADV_ctl'";
oVAR_CONNECTOR.statementPrepare(sVAR_TMP_SQL);
oVAR_CONNECTOR.statementExecuteUpdate();
oVAR_CONNECTOR.transactionCommit();
//Post session
oVAR_CONNECTOR.disconnect();
```
