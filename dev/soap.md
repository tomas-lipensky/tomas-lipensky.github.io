# SOAP

[curl](http://dasunhegoda.com/make-soap-request-command-line-curl/596/) --header "Content-Type: text/xml;charset=UTF-8" --header "SOAPAction: ACTION_YOU_WANT_TO_CALL" --data @FILE_NAME URL_OF_THE_SOAP_WEB_SERVICE_ENDPOINT  
curl --header "Content-Type: text/xml;charset=UTF-8" --header "SOAPAction:urn:GetVehicleLimitedInfo" --data @request.xml http://11.22.33.231:9080/VehicleInfoQueryService.asmx  
curl  -c c.cookies -b c.cookies -k --header "Content-Type: text/xml;charset=UTF-8" --header 'SOAPAction: "urn:internalvim25/5.5"' --data '<env:Envelope xmlns:xsd="http:*www.w3.org/2001/XMLSchema" xmlns:env="http:*schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http:*www.w3.org/2001/XMLSchema-instance|<env:Body><Login xmlns="urn:vim25|<_this type="SessionManager|SessionManager</_this><userName>#USER</userName><password>#PASSWD</password></Login></env:Body></env:Envelope>' https:*11.22.33.231/sdk  

### Nastroje

[SoapUI]() ... Soap User interface na emulaci SOAP dotazu a odpovedi
