<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>International SMS</h1> 

**Notification > Notification Hub > Usage Policy and Preset Guide > International SMS**

## Main Guidance

### Country-specific sender number
Check the main points below when sending international SMS messages.

* International SMS messages are sent in accordance with country-specific sender number policies and can be treated as spam if you do not follow them.
* The sender number set by the customer cannot guarantee exposure to the receiving terminal and may be changed to any number, text, NHN corporation, etc. to send international SMS messages normally.

### Send International SMS
* For detailed policies by country, please refer to **Detailed SMS Delivery Guide by country** below.
  * [National SMS Delivery Detail Guide Shortcut](https://nhnnotification.imweb.me/Technology/?q=YToxOntzOjEyOiJrZXl3b3JkX3R5cGUiO3M6MzoiYWxsIjt9&bmode=view&idx=17226410&t=board)
* In countries with strict international SMS message policies, such as China and Vietnam, messages can only be sent normally if the message is sent with an Authentication Number (OTP).
* We recommend that you enter an authentication number (OTP) for the message to be sent normally, as in the example (for example, your verification code is 00000)
* If you wish to send a marketing message, please contact **Customer Center**>**1:1 Contact** in advance.
  * [1:1 Inquiry Shortcut](https://www.nhncloud.com/kr/support/inquiry)
* In order to send international SMS messages normally, up to 12 characters of each country's policy can be added to the message and sent, which is included in the number of charged characters.
* In the case of overseas mobile carriers, it is difficult to check the exact cause of non-reception depending on the time of inquiry because the delivery log is only kept for approximately 7 days.
* Country-specific transmission quality is affected by your country's network and infrastructure environment and may differ from your domestic environment.

### International SMS Billing
* The cost of sending international SMS messages will be charged depending on the success or failure of data transmission to overseas carriers.
* The terminal reception result means successful data transmission to an overseas communication service provider and may differ from the actual terminal reception result. Even if the actual user did not receive the message, it may be included in the billing list.
* International SMS can be sent as long messages through the concatenated message feature. When connected by long messages, they will be charged by the number of characters sent.
* When applied to concatenated messages, the number of characters that can be sent is reduced in part as the header for connecting messages is processed.
* Character count and concatenated message standards are in accordance with international SMS standards.
* Messages sent by the concatenated message can also be received by the device in the form of several short messages rather than long ones, depending on mobile carrier and device policies.
* The number of charges per message can be checked in the messageCount field of the console detailed inquiry and detailed inquiry api.

| Encoding | Charge for 1 case | Charge for 2 cases | Charge for 3 cases | Charge for 4 cases | Charge for 5 cases |
| --- | --- | --- | --- | --- | --- |
| UCS-2<br>(Unicode) | 70 characters | 134 characters<br>(=67*2) | 201 characters<br>(=67*3) | 268 characters<br>(=67*4) | 335 characters<br>(=67*5) |
| GSM-7bit | 160 characters | 306 characters<br>(=153*2) | 459 characters<br>(=153*3) | 612 characters<br>(=153*4) | 765 characters<br>(=153*5) |

### Precautions - International SMS Mass Volume Pumping
* Some overseas mobile carriers (MNOs) artificially induce message sending to increase sales.
* On pages such as requesting a membership authentication number, a bot or abuser requests a large volume of messages to be sent.
* Most bots or abusers do not perform actual verification after a verification request. When abusing occurs, verification number requests increase, but the rate at which authentication is performed and converted is reduced.
* Notes
    * In the event of international SMS mass volume pumping, some or all international SMS volumes can be blocked without prior notice to the project. 
    * NHN Cloud is not responsible for any damage caused by abuse or blocking. Be careful about confidential information leakage and abuse.
* Recommended Measures
    * Select the country you want to allow and set the maximum monthly shipment through**Send international SMS messages setting**.


## Available Countries 

| Country name | Country code |
| ------- | ----- |
| United States / Canada | 1 |
| Russia / Kazakhstan | 7 |
| Egypt | 20 |
| Republic of South Africa | 27 |
| Greece | 30 |
| Netherlands | 31 |
| Belgium | 32 |
| France | 33 |
| Spain | 34 |
| Hungary | 36 |
| Italy | 39 |
| Romania | 40 |
| Switzerland | 41 |
| Austria | 43 |
| United Kingdom | 44 |
| Denmark | 45 |
| Sweden | 46 |
| Norway | 47 |
| Poland | 48 |
| Germany | 49 |
| Peru | 51 |
| Mexico | 52 |
| Cuba | 53 |
| Argentina | 54 |
| Brazil | 55 |
| Chile | 56 |
| Colombia | 57 |
| Venezuela | 58 |
| Malaysia | 60 |
| Australia | 61 |
| Indonesia | 62 |
| Philippines | 63 |
| New Zealand | 64 |
| Singapore | 65 |
| Thailand | 66 |
| Japan | 81 |
| Vietnam | 84 |
| China | 86 |
| Turkey | 90 |
| India | 91 |
| Pakistan | 92 |
| Afghanistan | 93 |
| Sri Lanka | 94 |
| Myanmar | 95 |
| Iran | 98 |
| South Sudan | 211 |
| Morocco | 212 |
| Algeria | 213 |
| Tunisia | 216 |
| Libya | 218 |
| Gambia | 220 |
| Senegal | 221 |
| Mauritania | 222 |
| Mali | 223 |
| Guinea | 224 |
| Côte d'Ivoire | 225 |
| Burkina Faso | 226 |
| Niger | 227 |
| Togo | 228 |
| Benin | 229 |
| Mauritius | 230 |
| Liberia | 231 |
| Sierra Leone | 232 |
| Ghana | 233 |
| Nigeria | 234 |
| Chad | 235 |
| Central African Republic | 236 |
| Cameroon | 237 |
| Cape Verde | 238 |
| S. Tomé & Principe | 239 |
| Equatorial Guinea | 240 |
| Gabon | 241 |
| Congo | 242 |
| Democratic Republic of the Congo | 243 |
| Angola | 244 |
| Guinea-Bissau | 245 |
| Seychelles | 248 |
| Sudan | 249 |
| Rwanda | 250 |
| Ethiopia | 251 |
| Somalia | 252 |
| Djibouti | 253 |
| Kenya | 254 |
| Tanzania | 255 |
| Uganda | 256 |
| Burundi | 257 |
| Mozambique | 258 |
| Zambia | 260 |
| Madagascar | 261 |
| Réunion Island | 262 |
| Zimbabwe | 263 |
| Namibia | 264 |
| Malawi | 265 |
| Lesotho | 266 |
| Botswana | 267 |
| Swaziland | 268 |
| Mayotte/Comoros | 269 |
| British St Helena | 290 |
| Eritrea | 291 |
| Aruba | 297 |
| Faroe Islands | 298 |
| Greenland | 299 |
| Gibraltar | 350 |
| Portugal | 351 |
| Luxembourg | 352 |
| Ireland | 353 |
| Iceland | 354 |
| Albania | 355 |
| Malta | 356 |
| Cyprus | 357 |
| Finland | 358 |
| Bulgaria | 359 |
| Lithuania | 370 |
| Latvia | 371 |
| Estonia | 372 |
| Moldova | 373 |
| Armenia | 374 |
| Belarus | 375 |
| Andorra | 376 |
| Monaco | 377 |
| San Marino | 378 |
| Ukraine | 380 |
| Serbia | 381 |
| Montenegro | 382 |
| Republic of Kosovo | 383 |
| Croatia | 385 |
| Slovenia | 386 |
| Bosnia and Herzegovina | 387 |
| North Macedonia | 389 |
| Czechia | 420 |
| Slovakia | 421 |
| Liechtenstein | 423 |
| British Falkland Islands | 500 |
| Belize | 501 |
| Guatemala | 502 |
| El Salvador | 503 |
| Honduras | 504 |
| Nicaragua | 505 |
| Costa Rica | 506 |
| Panama | 507 |
| St. Pierre & Miquelon | 508 |
| Haiti | 509 |
| Guadeloupe | 590 |
| Bolivia | 591 |
| Guyana | 592 |
| Ecuador | 593 |
| French Guiana | 594 |
| Paraguay | 595 |
| Martinique | 596 |
| Suriname | 597 |
| Uruguay | 598 |
| Dutch Antilles/Curiaso | 599 |
| Timor-Leste | 670 |
| Brunei Darussalam | 673 |
| Nauru | 674 |
| Papua New Guinea | 675 |
| Tonga | 676 |
| Solomon Islands | 677 |
| Vanuatu | 678 |
| Fiji | 679 |
| Palau | 680 |
| French Wallis Putuna Islands | 681 |
| Cocos Keeling Islands (Cook Islands) | 682 |
| Samoa | 685 |
| Kiribati | 686 |
| New Caledonia | 687 |
| French Polynesia | 689 |
| Micronesia | 691 |
| Marshall Islands | 692 |
| Hong-Kong | 852 |
| Macau | 853 |
| Cambodia | 855 |
| Laos | 856 |
| Bangladesh | 880 |
| Taiwan | 886 |
| Maldives | 960 |
| Lebanon | 961 |
| Jordan | 962 |
| Syria | 963 |
| Iraq | 964 |
| Kuwait | 965 |
| Saudi Arabia | 966 |
| Yemen | 967 |
| Oman | 968 |
| Palestine | 970 |
| United Arab Emirates | 971 |
| Israel | 972 |
| Bahrain | 973 |
| Qatar | 974 |
| Bhutan | 975 |
| Mongolia | 976 |
| Nepal | 977 |
| Tajikistan | 992 |
| Turkmenistan | 993 |
| Azerbaijan | 994 |
| Georgia | 995 |
| - Requires pre-registration of the sending number and fails to send the message if not registered | 996 |
| Uzbekistan | 998 |
| Bahamas | 1242 |
| Barbados | 1246 |
| Anguilla | 1264 |
| Antigua & Barbuda | 1268 |
| Virgin Islands (US) | 1284 |
| British Virgin Islands | 1340 |
| Cayman Islands | 1345 |
| Bermuda | 1441 |
| Grenada | 1473 |
| Turks & Caicos Is. | 1649 |
| Montserrat | 1664 |
| Northern Marianas | 1670 |
| Guam | 1671 |
| American Samoa | 1684 |
| St. Lucia | 1758 |
| Dominica | 1767 |
| St. Vincent and the Grenadines | 1784 |
| Puerto Rico | 1787, 1939 |
| Dominican Republic | 1809, 1829, 1849 |
| Trinidad & Tobago Rep. | 1868 |
| St. Kitts and Nevis | 1869 |
| Jamaica | 1876 |


