<div align="center">

## Country Based Redirection


</div>

### Description

'redirect users based on which country they are visiting your website from.
 
### More Info
 
NetGeo

http://www.caida.org/tools/utilities/netgeo/


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[dvchaos](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/dvchaos.md)
**Level**          |Beginner
**User Rating**    |4.7 (14 globes from 3 users)
**Compatibility**  |ASP \(Active Server Pages\), HTML, VbScript \(browser/client side\)

**Category**       |[Complete Applications](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/complete-applications__4-7.md)
**World**          |[ASP / VbScript](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/asp-vbscript.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/dvchaos-country-based-redirection__4-7408/archive/master.zip)

### API Declarations

use and abuse.


### Source Code

```
<%
'redirect users based on which country they are calling from.
'uses CAIDA's NetGeo at http://www.caida.org/tools/utilities/netgeo/
'if you find this code usefull please vote !
Dim clientIP
Dim strURL
ClientIP = Request.ServerVariables("HTTP_X_FORWARDED_FOR")
If ClientIP = "" Then
	ClientIP = Request.ServerVariables("REMOTE_ADDR")
End If
strURL="http://netgeo.caida.org/perl/netgeo.cgi?target=" & clientIP
	Dim objXML
	Set objXML = CreateObject("Msxml2.XMLHTTP")
  'if this code creates a 500 internal server error
  'it is most likely because of the above set obj line.
  'that means the Microsoft XML parser engine is either
  'not installed on your web host's servers or simply
  'that they have a different version installed.
  'in any case you should contact your web server ISP
  'and find out exactly which version(if any) they have
  'installed.
	objXML.open "GET", strURL, false
	objXML.send
	strResponse = objXML.responseText
 	set objXML = Nothing
  dim ClientCountry
	if instr(strResponse,"TARGET: ") then
		X = instr(strResponse,"TARGET: ")
		strResponse = mid(StrResponse,x,len(StrResponse))
	end if
	ClientCountry = strResponse
	'Retain the original strResponse Content for possible further
	'use since NetGeo returns more than just Country Codes.
  '(see http://www.timesafe.uk.com/whereisyou.asp )
	if instr(ClientCountry,"COUNTRY: ") then
		X = instr(ClientCountry,"COUNTRY: ")
		ClientCountry = mid(ClientCountry,x+15,len(ClientCountry))
		X = instr(ClientCountry,"<br>")
		ClientCountry = mid(ClientCountry,1,x-1)
	end if
Select Case ClientCountry
case "UK"
Response.redirect "http://www.google.co.uk/"
case "US"
Response.redirect "http://www.google.com/"
Case Else
Response.redirect "http://www.altavista.com/"
End select
'Here is a list of 243 Country Code Abbreviations and their Appropriate Human Readable Country Names
'as used by NetGeo ( http://www.caida.org/tools/utilities/netgeo/ )
'This countrycode list is available as a Microsoft Access 2000 database at
'http://www.timesafe.uk.com/countrycodes.mdb
'AD Andorra
'AE United Arab Emirates
'AF Afghanistan
'AG Antigua and Barbuda
'AI Anguilla
'AL Albania
'AM Armenia
'AN Netherlands Antilles
'AO Angola
'AQ Antarctica
'AR Argentina
'AS American Samoa
'AT Austria
'AU Australia
'AW Aruba
'AZ Azerbaijan
'BA Bosnia and Herzegovina
'BB Barbados
'BD Bangladesh
'BE Belgium
'BF Burkina Faso
'BG Bulgaria
'BH Bahrain
'BI Burundi
'BJ Benin
'BM Bermuda
'BN Brunei Darussalam
'BO Bolivia
'BR Brazil
'BS Bahamas
'BT Bhutan
'BV Bouvet Island
'BW Botswana
'BY Belarus
'BZ Belize
'CA Canada
'CC Cocos (Keeling) Islands
'CF Central African Republic
'CG Congo
'CH Switzerland
'CI Cote D'Ivoire (Ivory Coast)
'CK Cook Islands
'CL Chile
'CM Cameroon
'CN China
'CO Colombia
'CR Costa Rica
'CS Czechoslovakia (former)
'CU Cuba
'CV Cape Verde
'CX Christmas Island
'CY Cyprus
'CZ Czech Republic
'DE Germany
'DJ Djibouti
'DK Denmark
'DM Dominica
'DO Dominican Republic
'DZ Algeria
'EC Ecuador
'EE Estonia
'EG Egypt
'EH Western Sahara
'ER Eritrea
'ES Spain
'ET Ethiopia
'FI Finland
'FJ Fiji
'FK Falkland Islands (Malvinas)
'FM Micronesia
'FO Faroe Islands
'FR France
'FX France, Metropolitan
'GA Gabon
'GB Great Britain (UK)
'GD Grenada
'GE Georgia
'GF French Guiana
'GH Ghana
'GI Gibraltar
'GL Greenland
'GM Gambia
'GN Guinea
'GP Guadeloupe
'GQ Equatorial Guinea
'GR Greece
'GS S. Georgia and S. Sandwich Isls.
'GT Guatemala
'GU Guam
'GW Guinea-Bissau
'GY Guyana
'HK Hong Kong
'HM Heard and McDonald Islands
'HN Honduras
'HR Croatia (Hrvatska)
'HT Haiti
'HU Hungary
'ID Indonesia
'IE Ireland
'IL Israel
'IN India
'IO British Indian Ocean Territory
'IQ Iraq
'IR Iran
'IS Iceland
'IT Italy
'JM Jamaica
'JO Jordan
'JP Japan
'KE Kenya
'KG Kyrgyzstan
'KH Cambodia
'KI Kiribati
'KM Comoros
'KN Saint Kitts and Nevis
'KP Korea (North)
'KR Korea (South)
'KW Kuwait
'KY Cayman Islands
'KZ Kazakhstan
'LA Laos
'LB Lebanon
'LC Saint Lucia
'LI Liechtenstein
'LK Sri Lanka
'LR Liberia
'LS Lesotho
'LT Lithuania
'LU Luxembourg
'LV Latvia
'LY Libya
'MA Morocco
'MC Monaco
'MD Moldova
'MG Madagascar
'MH Marshall Islands
'MK Macedonia
'ML Mali
'MM Myanmar
'MN Mongolia
'MO Macau
'MP Northern Mariana Islands
'MQ Martinique
'MR Mauritania
'MS Montserrat
'MT Malta
'MU Mauritius
'MV Maldives
'MW Malawi
'MX Mexico
'MY Malaysia
'MZ Mozambique
'NA Namibia
'NC New Caledonia
'NE Niger
'NF Norfolk Island
'NG Nigeria
'NI Nicaragua
'NL Netherlands
'NO Norway
'NP Nepal
'NR Nauru
'NT Neutral Zone
'NU Niue
'NZ New Zealand (Aotearoa)
'OM Oman
'PA Panama
'PE Peru
'PF French Polynesia
'PG Papua New Guinea
'PH Philippines
'PK Pakistan
'PL Poland
'PM St. Pierre and Miquelon
'PN Pitcairn
'PR Puerto Rico
'PT Portugal
'PW Palau
'PY Paraguay
'QA Qatar
'RE Reunion
'RO Romania
'RU Russian Federation
'RW Rwanda
'SA Saudi Arabia
'Sb Solomon Islands
'SC Seychelles
'SD Sudan
'SE Sweden
'SG Singapore
'SH St. Helena
'SI Slovenia
'SJ Svalbard and Jan Mayen Islands
'SK Slovak Republic
'SL Sierra Leone
'SM San Marino
'SN Senegal
'SO Somalia
'SR Suriname
'ST Sao Tome and Principe
'SU USSR (former)
'SV El Salvador
'SY Syria
'SZ Swaziland
'TC Turks and Caicos Islands
'TD Chad
'TF French Southern Territories
'TG Togo
'TH Thailand
'TJ Tajikistan
'TK Tokelau
'TM Turkmenistan
'TN Tunisia
'TO Tonga
'TP East Timor
'TR Turkey
'TT Trinidad and Tobago
'TV Tuvalu
'TW Taiwan
'TZ Tanzania
'UA Ukraine
'UG Uganda
'UK United Kingdom
'UM US Minor Outlying Islands
'US United States
'UY Uruguay
'UZ Uzbekistan
'VA Vatican City State (Holy See)
'VC Saint Vincent and the Grenadines
'VE Venezuela
'VG Virgin Islands (British)
'VI Virgin Islands (U.S.)
'VN Viet Nam
'VU Vanuatu
'WF Wallis and Futuna Islands
'WS Samoa
'YE Yemen
'YT Mayotte
'YU Yugoslavia
'ZA South Africa
'ZM Zambia
'ZR Zaire
'ZW Zimbabwe
%>
```

