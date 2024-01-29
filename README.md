# Asterisk-multi-tenant-architecture
Creating a working platform to manage multiple SIP number for different companies for cloud PBX system

exten => _X.,1,Set(Var_TO=${CUT(CUT(SIP_HEADER(To),@,1),:,2)})
exten => _X.,1: This part defines the extension pattern. The _X. is a wildcard pattern that matches any digit (_X) followed by any number of digits (.). The 1 is the priority of the extension, meaning it is the first step to be executed.

Set(Var_TO=${CUT(CUT(SIP_HEADER(To),@,1),:,2)}): This part sets the variable Var_TO. Let's break down the nested functions:

SIP_HEADER(To): Retrieves the SIP header field "To" from the incoming SIP request.
CUT(SIP_HEADER(To),@,1): Cuts the string obtained from the "To" header at the '@' symbol, and selects the first part.
CUT(CUT(SIP_HEADER(To),@,1),:,2): Cuts the result obtained from the previous step at the ':' symbol and selects the second part.
The final result is assigned to the variable Var_TO.
In summary, this line is extracting a portion of the "To" header from an incoming SIP request and storing it in the Var_TO variable. It looks like it's trying to extract the username part of the SIP URI after the '@' symbol and before the ':' symbol. For example, if the "To" header is like "sip:user@example.com:5060", then Var_TO would be set to "user".
