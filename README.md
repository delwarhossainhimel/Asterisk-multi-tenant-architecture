# Asterisk-multi-tenant-architecture 
# Asterisk 18.17.0
Creating a working platform to manage multiple SIP number for different companies in cloud PBX system

exten => _X.,1,Set(Var_TO=${CUT(CUT(SIP_HEADER(To),@,1),:,2)})
exten => _X.,1: This part defines the extension pattern. The _X. is a wildcard pattern that matches any digit (_X) followed by any number of digits (.). The 1 is the priority of the extension, meaning it is the first step to be executed.

Set(Var_TO=${CUT(CUT(SIP_HEADER(To),@,1),:,2)}): This part sets the variable Var_TO. Let's break down the nested functions:

SIP_HEADER(To): Retrieves the SIP header field "To" from the incoming SIP request.
CUT(SIP_HEADER(To),@,1): Cuts the string obtained from the "To" header at the '@' symbol, and selects the first part.
CUT(CUT(SIP_HEADER(To),@,1),:,2): Cuts the result obtained from the previous step at the ':' symbol and selects the second part.
The final result is assigned to the variable Var_TO.
In summary, this line is extracting a portion of the "To" header from an incoming SIP request and storing it in the Var_TO variable. It looks like it's trying to extract the username part of the SIP URI after the '@' symbol and before the ':' symbol. For example, if the "To" header is like "sip:user@example.com:5060", then Var_TO would be set to "user".


same => n,GotoIf($["${Var_TO}" = ""sip_number"]?contestname,s,1:3)
same => n: This indicates that the next priority in the current extension will have the same numeric label as the previous one. It is commonly used in Asterisk dialplan to continue the sequence of priorities.

GotoIf($["${Var_TO}" = "sip_number"]?contestname,s,1:3): This is a conditional jump using the GotoIf application. It checks whether the value of the variable Var_TO is equal to the string "9613845676". If the condition is true, it jumps to the label contestname,s,1; otherwise, it jumps to priority 3.

Explanation of the condition:

$["${Var_TO}" = "sip_number"]: This is a conditional expression that checks if the value of the variable Var_TO is equal to the string "sipnumber".
Explanation of the jump destinations:

If the condition is true (?), it jumps to contestname,s,1.
If the condition is false (:), it jumps to priority 3.
So, in plain English, this line is saying: "If the value of Var_TO is equal to 'sip_number', jump to the label contestname,s,1; otherwise, jump to priority 3."
