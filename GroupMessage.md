# Group Message Data

## Message #1

Use key 'Jim Test 1' - Enitity #1

~~~
AAD =  85-01-84-0A-26-82-81-02-82-02-01-82-02-01-41-E1-41-01-40
    [1, [10, -7, [[2], [2, 1]], [2, 1]], h'E1', h'01', h'']
      
IV = FA-FA-67-D4-F5-1E-7A-62-E9-39-D2-21-0A
Sender Key = DB-DB-DC-B0-BD-08-CE-B9-D3-CF-51-69-AA-F9-C9-D9

Signature AAD = 86-01-84-0A-26-82-81-02-82-02-01-82-02-01-41-E1-41-01-40-47-39-01-03-0A-0B-0C-E1
          [1, [10, -7, [[2], [2, 1]], [2, 1]], h'E1', h'01', h'', h'3901030A0B0CE1']

ToBeSigned = "85-71-43-6F-75-6E-74-65-72-53-69-67-6E-61-74-75-72-65-30-40-40-58-1B-86-01-84-0A-26-82-81-02-82-02-01-82-02-01-41-E1-41-01-40-47-39-01-03-0A-0B-0C-E1-4D-F0-A0-FB-E1-AE-80-E9-24-C9-0E-04-42-7D"
           ["CounterSignature0", h'', h'', h'8601840A2682810282020182020141E1410140473901030A0B0CE1', h'F0A0FBE1AE80E924C90E04427D']


Payload = F0-A0-FB-E1-AE-80-E9-24-C9-0E-04-42-7D-CC-73-DA-94-00-8E-CD-54-DB-98-DA-4F-F1-71-F8-23-C5-EB-D4-6C-78-BD-C7-9C-D8-D9-19-E6-CC-25-F2-90-69-26-0E-71-53-9E-F7-6A-E9-0A-58-EE-FF-BB-C2-0C-EE-0A-12-D1-33-44-18-34-92-25-CD-E8-16-4E-F0-8E

Encoded Request = 40-02-FF-FF-97-39-01-03-0A-0B-0C-E1-FF-F0-A0-FB-E1-AE-80-E9-24-C9-0E-04-42-7D-CC-73-DA-94-00-8E-CD-54-DB-98-DA-4F-F1-71-F8-23-C5-EB-D4-6C-78-BD-C7-9C-D8-D9-19-E6-CC-25-F2-90-69-26-0E-71-53-9E-F7-6A-E9-0A-58-EE-FF-BB-C2-0C-EE-0A-12-D1-33-44-18-34-92-25-CD-E8-16-4E-F0-8E
~~~

> Rikard: Using Jim Test 1 - Entity 1, but with ID Context '0A0B0C' I see in the OSCORE option and KID E1.
> I can calculate and get the exact same values for AAD, IV, Sender Key and Signature AAD.
> However trying to receive it as an incoming request the decryption works but the Countersignature verification fails.

> JLS: I have updated the context and entity IDs in the keys file so they are consistent with what I am using.
> I added a ToBeSigned field which is the COSE ToBeSigned

>Rikard: I understand what was going wrong now. This is the ToBeSigned I got:
~~~
["CounterSignature0", null, h'', h'8601840A2682810282020182020141E1410140473901030A0B0CE1', h'F0A0FBE1AE80E924C90E04427D']
~~~
> Rikard: It seems during my work on adding the COSE code needed for Group OSCORE to the existing COSE code that was in OSCORE I missed something, which made the body protected field be null rather than an empty byte array. (I have been doing some work to integrate the Group OSCORE code based on a fork of Californium.).  
> I have now fixed this and can successfully decrypt your message 1 and the countersignature verification works.


## Message #2

Use key 'Rikard Test 1' - Entity #1

~~~
AAD =  85-01-84-0A-26-82-81-02-82-02-01-82-02-01-41-01-41-00-40
    [1, [10, -7, [[2], [2, 1]], [2, 1]], h'01', h'00', h'']
      
IV = 2D-A5-8F-B8-5F-F1-B8-1D-0B-71-81-B8-5E
Sender Key = E3-9A-0C-7C-77-B4-3F-03-B4-B3-9A-B9-A2-68-69-9F

Signature AAD = 86-01-84-0A-26-82-81-02-82-02-01-82-02-01-41-01-41-00-40-4C-39-00-08-37-CB-F3-21-00-17-A2-D3-01
          [1, [10, -7, [[2], [2, 1]], [2, 1]], h'01', h'00', h'', h'39000837CBF3210017A2D301']
          
ToBeSigned = 85-71-43-6F-75-6E-74-65-72-53-69-67-6E-61-74-75-72-65-30-40-40-58-20-86-01-84-0A-26-82-81-02-82-02-01-82-02-01-41-01-41-00-40-4C-39-00-08-37-CB-F3-21-00-17-A2-D3-01-49-96-3F-FA-3C-DF-9E-D8-FA-C0
           ["CounterSignature0", h'', h'', h'8601840A2682810282020182020141014100404C39000837CBF3210017A2D301', h'963FFA3CDF9ED8FAC0']

Payload = 96-3F-FA-3C-DF-9E-D8-FA-C0-9E-33-E6-FF-82-91-CD-3C-CA-52-38-3B-7E-24-B1-47-4E-AC-7C-63-D3-2C-8C-30-EA-DB-5D-98-70-A9-1D-67-9E-9F-14-82-97-F7-0B-62-D9-4B-3B-19-2C-4C-06-71-87-20-86-46-D2-7D-26-09-94-82-C0-43-D4-F9-AD-00

Encoded Request = 54-02-FF-FF-34-73-12-11-9C-39-00-08-37-CB-F3-21-00-17-A2-D3-01-FF-96-3F-FA-3C-DF-9E-D8-FA-C0-9E-33-E6-FF-82-91-CD-3C-CA-52-38-3B-7E-24-B1-47-4E-AC-7C-63-D3-2C-8C-30-EA-DB-5D-98-70-A9-1D-67-9E-9F-14-82-97-F7-0B-62-D9-4B-3B-19-2C-4C-06-71-87-20-86-46-D2-7D-26-09-94-82-C0-43-D4-F9-AD-00
~~~

> JLS: Well, I have not checked the decryption part because I do signature validation first, but I cannot validate you signature either.
>  The to be signed value I got was.
>  As with you I successfully decrypted your message.
~~~
85-71-43-6F-75-6E-74-65-72-53-69-67-6E-61-74-75-72-65-30-40-40-58-20-86-01-84-0A-26-82-81-02-82-02-01-82-02-01-41-01-41-00-40-4C-39-00-08-37-CB-F3-21-00-17-A2-D3-01-49-96-3F-FA-3C-DF-9E-D8-FA-C0

["CounterSignature0", h'', h'', h'8601840A2682810282020182020141014100404C39000837CBF3210017A2D301', h'963FFA3CDF9ED8FAC0']
~~~

> Rikard: As mentioned above I fixed the issue with the to-be-signed data. I have now updated my message contents with re-generated values after this fix. Only the payload and encoded request should be different.

## Message #3

Use key 'Rikard Test 2' - Entity #1

~~~
AAD =  85-01-84-0A-27-82-81-01-82-01-06-82-01-06-41-0A-41-01-40
    [1, [10, -8, [[1], [1, 6]], [1, 6]], h'0A', h'01', h'']
      
IV = 17-65-5E-BD-E5-09-8E-0D-46-A6-E9-DA-A2
Sender Key = 33-BA-DB-4D-6B-48-7E-16-BC-8D-C3-F6-DB-38-29-90

Signature AAD = 86-01-84-0A-27-82-81-01-82-01-06-82-01-06-41-0A-41-01-40-46-39-01-02-DD-11-0A
          [1, [10, -8, [[1], [1, 6]], [1, 6]], h'0A', h'01', h'', h'390102DD110A']
          
ToBeSigned = 85-71-43-6F-75-6E-74-65-72-53-69-67-6E-61-74-75-72-65-30-40-40-58-1A-86-01-84-0A-27-82-81-01-82-01-06-82-01-06-41-0A-41-01-40-46-39-01-02-DD-11-0A-49-42-41-71-AB-DF-18-40-50-29
           ["CounterSignature0", h'', h'', h'8601840A27828101820106820106410A41014046390102DD110A', h'424171ABDF18405029']

Payload = 42-41-71-AB-DF-18-40-50-29-79-42-02-2C-7A-85-E1-75-17-24-6B-31-DB-B1-0C-50-78-73-0E-9D-08-57-E3-EA-0A-63-0F-AF-D1-B2-24-23-64-7E-C0-9A-5D-60-C7-4F-1A-45-B2-95-DB-10-D5-56-9D-6D-A0-9F-44-3E-79-2D-6A-72-BF-BC-72-E3-2C-0D

Encoded Request = 58-02-FF-FF-11-84-AF-72-82-CE-23-BA-96-39-01-02-DD-11-0A-FF-42-41-71-AB-DF-18-40-50-29-79-42-02-2C-7A-85-E1-75-17-24-6B-31-DB-B1-0C-50-78-73-0E-9D-08-57-E3-EA-0A-63-0F-AF-D1-B2-24-23-64-7E-C0-9A-5D-60-C7-4F-1A-45-B2-95-DB-10-D5-56-9D-6D-A0-9F-44-3E-79-2D-6A-72-BF-BC-72-E3-2C-0D
~~~

