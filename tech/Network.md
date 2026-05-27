**Network**

Your router assigns IP addresses to devices on your network using [DHCP](https://www.pcmag.com/encyclopedia/term/dhcp), or Dynamic Host Configuration Protocol. As you connect new devices to the network, they'll be assigned the next IP address in the pool, and if a device hasn't connected in a few days, its IP address will "expire" so it can be assigned to something else.

Instead of letting your router assign whatever IP address is free at any given time, you can assign specific IP addresses to the devices you access frequently. For example, I have my home server set to 192.168.1.10.You can assign these static IP addresses on the device itself—using, say, Windows' network settings on each computer—or you can do it at the router level. Doing it at the router level is called assigning a DHCP reservation, though manypeople (and even some [routers](https://www.pcmag.com/picks/the-best-wireless-routers)) still refer to it as a "static IP address." For DHCP reservation On your router's config page, enter an easy-to-remember label for the device (like "Whitson's Desktop PC"), the MAC address, and your desired IP address. Save your changes, and repeat the process for any other IP addresses you want to reserve.

A Local Area Network (LAN) might be as big as several buildings or as small as a home. Everyone connected to the LAN is in the same physical location.

In a LAN, the router assigns each device its own unique internal IP address. They follow a pattern as follows:

- 10.0.0.0 /8 (10.x.x.x)
- 172.16.0.0 /12 (172.16.x.x - 172.31.x.x)
- 192.168.0.0 /16 (192.168.x.x)

These addresses are only visible inside a network, between devices, and are considered private from outside networks. There are potentially millions of locations that might have the same pool of internal IP addresses as your business. It doesn't negatively affect your addressing scheme, as they are only used within their own private network, and hence, there is no conflict. There are special configurations that can be done, but there are some standard things to keep in mind. In order for the devices in the network to communicate with each other, they should all follow the same pattern as the other devices. They should also be on the same subnet, which is the organizational method within the IP addressing scheme. Each IP address must also be unique. You should never see any of these addresses in this pattern as a public IP address, as they are reserved for private LAN addresses only.

All of these devices send data through a default gateway (a router) to move data out to the Internet. When the default gateway receives the information, it needs to do Network Address Translation (NAT), which encapsulates the IP address to be publicly facing. Since anything going out across the Internet needs a public IP address, this encapsulation ensures the data can find its way back to the requestor.

You can configure the internal IP address to stay the same by configuring static DHCP on the router or assign a static IP address on the device itself. From that point forward, that device will keep the same IP address unless manually changed or if the router is reset to factory default.

- If the same static IP addresses are assigned to two different devices they will both be unable to communicate on the network. This can be prevented if the administrator has kept good notes on the topology of the network.
- If DHCP assigns an IP address that is already assigned as a static IP address, those devices can’t communicate. The solution for this problem is to assign blocks of IP addresses for DHCP and different blocks for static addressing.

**When assigning static IP addresses:**

1. Reserve a block of addresses for DHCP and a separate block for static addressing.
1. Only use addresses from the 10.0.0.0 /8 (10.x.x.x), 172.16.0.0 /12 (172.16.x.x - 172.31.x.x), or 192.168.0.0 /16 (192.168.x.x) pattern.
1. Do not use an address that ends in .0 as those are typically reserved for networks.
1. Do not use an address that ends in .1 or .254, as those are often the default IP addresses of devices. The first or last usable IP address of a network is so common that a hacker would most likely use it to try to access the network.
1. Do not use the last IP address of the IP Network pool, ending in .255, as they are reserved for the broadcast address.

Computers use IP addresses to communicate over TCP/IP.

Windows Server 2008 provides the following ways to configure IP addressing:

- **Manually** IP addresses that are assigned manually are called static IP addresses. Static IP addresses are fixed and don’t change unless you change them. You’ll usually assign static IP addresses to Windows servers, and when you do this, you’ll need to configure additional information to help the server navigate the network.
- **Dynamically** A DHCP server (if one is installed on the network) assigns dynamic IP addresses at startup, and the addresses might change over time. Dynamic IP addressing is the default configuration.
- **Alternatively (IPv4 only)** When a computer is configured to use DHCPv4 and no DHCPv4 server is available, Windows Server 2008 assigns an alternate private IP address automatically. By default, the alternate IPv4 address is in the range from 169.254.0.1 to 169.254.255.254 with a subnet mask of 255.255.0.0. You can also specify a user-configured alternate IPv4 address, which is particularly useful for laptop users.

  IPv6 addresses and IPv4 addresses are very different. With IPv6, the first 64 bits represent the network ID and the remaining 64 bits represent the network interface. With IPv4, a variable number of the initial bits represent the network ID and the rest of the bits represent the host ID. For example, if you’re working with IPv4 and a computer on the network segment 192.168.10.0 with a subnet mask of 255.255.255.0, the first 24 bits represent the network ID and the address range you have available for computer hosts is from 192.168.10.1 to 192.168.10.254. In this range, the address 192.168.10.255 is reserved for network broadcasts.

  If you’re on a private network that is indirectly connected to the Internet, you should use private IPv4 addresses. Table 21-1 summarizes private network IPv4 addresses.

  Table 21-1. Private IPv4 Network Addressing

  |**Private Network ID**|**Subnet Mask**|**Network Address Range**|
  | :- | :- | :- |
  |10\.0.0.0|255\.0.0.0|10\.0.0.0–10.255.255.255|
  |172\.16.0.0|255\.240.0.0|172\.16.0.0–172.31.255.255|
  |192\.168.0.0|255\.255.0.0|192\.168.0.0–192.168.255.255|

  All other IPv4 network addresses are public and must be leased or purchased. If the network is connected directly to the Internet and you’ve obtained a range of IPv4 addresses from your Internet service provider, you can use the IPv4 addresses you’ve been assigned.

  Before you assign a static IP address, you should make sure that the address isn’t already in use or reserved for use with DHCP. With the PING command, you can check to see whether an address is in use. Open a command prompt and type **ping**, followed by the IP address you want to check.

  To test the IPv4 address 10.0.10.12, you would use the following command:

  ping 10.0.10.12

  To test the IPv6 address FEC0::02BC:FF:BECB:FE4F:961D, you would use the following command:

  ping FEC0::02BC:FF:BECB:FE4F:961D

  If you receive a successful reply from the PING test, the IP address is in use and you should try another one. If no current host on the network uses this IP address, the PING command output should be similar to the following:

  Pinging 192.168.1.100 with 32 bytes of data:

  Request timed out.

  Request timed out.

  Request timed out.

  Request timed out.

  Ping statistics for 192.168.1.100:

  Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)

  You can then use the IP address.

The Subnet Mask field ensures that the computer communicates over the network properly. Windows Server 2008 should insert a default value for the subnet prefix into the Subnet Mask text box. If the network doesn’t use variable-length subnetting, the default value should suffice. If your network does use variable-length subnets, you’ll need to change this value as appropriate for your network.

If the computer needs to access other TCP/IP networks, the Internet, or other subnets, you must specify a default gateway. Type the IP address of the network’s default router in the Default Gateway text box.

DNS is needed for domain name resolution. Select Use The Following DNS Server Addresses and then type a preferred address and an alternate DNS server address in the text boxes provided.

Many organizations use DHCP servers to dynamically assign IPv4 and IPv6 addresses. To receive an IPv4 or IPv6 address, client computers use a limited broadcast to advertise that they need to obtain an IP address. DHCP servers on the network acknowledge the request by offering the client an IP address. The client acknowledges the first offer it receives, and the DHCP server in turn tells the client that it has succeeded in leasing the IP address for a specified amount of time.

The message from the DHCP server can, and typically does, include the IP addresses of the default gateway, the preferred and alternate DNS servers, and the preferred and alternate WINS servers.

Dynamic IP addresses aren’t for all hosts on the network, however. Typically, you’ll want to assign dynamic IP addresses to workstations and, in some instances, member servers that perform noncritical roles on the network. But if you use dynamic IP addressing for member servers, these servers should have reservations for their IP addresses. For any server that has a critical network role or provides a key service, you’ll definitely want to use static IP addresses. Finally, with domain controllers and DHCP servers, you must use static IP addresses, so don’t try to assign dynamic IP addresses to these servers.


DNS is a host name resolution service that you can use to determine the IP address of a computer from its host name. This lets users work with host names, such as *http://www.msn.com* or *http://www.microsoft.com*, rather than an IP address, such as 192.168.5.102 or 192.168.12.68. DNS is the primary name service for Windows Server 2008 and the Internet.

Ip address is like a postal code a number to identify a device (network card) in the internal network or the Internet, this address in the local network or the Internet must be dedicated, that is, if the device works in the internal network, its IP address must be unique And it should not be duplicated elsewhere until the sent packets reach our desired destination (if the IP is duplicate, the so-called **Conflict** occurs.

Ip address is specified to the TCP/IP Protocol**.**

پروتکل **TCP/IP** یا **Transmission Control Protocol / Internet Protocol** به چندین دلیل بر سایر پروتکل ها در این زمینه پیشی گرفته است و امروزه به یکی از پر کاربرد ترین پروتکل ها در جهان تبدیل شده است. مهمترین دلایل برتری این پروتکل ویندوزی، امنیت بالا، سازگاری با روتر و کاربر آن در شبکه های بزرگ و همچنین شبکه های کوچک است. شکل کلی آن به صورت **W.X.Y.Z**   است. به هر یک از این حروف، **Octet**گفته میشود. در ضمن هر کدام از این حروف، در مبنای 10 می توانند تا 255 عدد گذاری شوند. بنابراین هر خانه در مبنای 2، 8 بیتی می شود و چون 4 خانه داریم، مجموعن 32 بیت می شود!

**IPخصوصی**

برای جلوگیری از هدردهی آی‌پی در هر کلاس، یک محدودهٔ آی‌پی برای شبکه‌های خصوصی (مانند شبکهٔ داخلی ادارات و شرکت‌ها) در نظر گرفته شده‌است

`  `**to    10.0.0.0      10.255.255.255**: این رنج برای استفاده در شبکه های محلی رزور شده است. با این رنج **1** شبکه به همراه **256\*256\*256** کامپیوتر خواهیم داشت. علت واضح است. در کلاس **A**، تنها **Octed** اول یعنی **W،** شماره شبکه(**Net ID**) است. چون در هر دو رنج، عدد **10** تغییر نکرده است بنابراین یک شبکه بیشتر نخواهیم داشت. تعداد کامپیوتر ها هم که سه **Octed** بعدی خواهد بود.
`  `**to   172.16.0.0 172.31.255.255**: باز هم برای استفاده در شبکه های محلی با این تفاوت که در این حالت **16** شبکه خواهیم داشت.


`   `**to   192.168.00.     192.168.255.255**     : این رنج هم برای استفاده ی **Local** با **255** شبکه. شاید بعضی از دوستان با این آدرس **IP** آشنا باشند. علت استفاده از این رنج همین است که در اینترنت از آن استفاده نمی شود و همچنین شبکه های بیشتری دارد و با وجود تعداد کمتر کامپیوتر در هر شبکه(نهایتن 255 کامپیوتر در هر شبکه)، **IP** ها را بی جهت مصرف نمی کند. یکی از اصول مهم، استفاده ی درست و به مقدار از آدرس های **IP** است که در شبکه های کوچک تا متوسط، رنج **192.168** کاملا جواب میدهد.

**127.0.0.1**: این **IP** هم در اینترنت وجود خارجی ندارد! **Loopback** کردن، **Ping** کردن و همچنین استفاده در **Troublesshooting**(اشکال زدایی) از کاربرد های این **IP** است!


**169.254.0.0**: به جای اون **0.0** شما **Y.Z** بگذارید. به این معنا که هر دو عدد تا **255** قابل مقدار دهی هستند. این **IP** یک کاربرد خاص دارد که گفتنش نیاز به توضیح فراوان دارد. البته در چند پست بعد، به احتمال زیاد در این مورد هم صحبت خواهیم کرد. اما فعلن همین قدر بس که این رنج هم در اینترنت وجود ندارد و برای اختصاص **IP** در حالت **APIPA** رزرو شده است.

[
](http://amirweb.me/wp-content/uploads/2013/12/400px-IP_Address_Classes.jpg)


برای یک ویندوز سرور برای وصل کردن کلاینت به سرور 

در سیستم کلاینت IP  که در بخش DNS وارد می شود همان IP سرور یا همان Domain می باشد که قصد داریم عضو آن Domain شویم.

بعد از تنظیم DNS نیاز هست که یکبار کانکشن رو بررسی کنیم که ببینیم آیا توانستیم با سرور ارتباط برقرار کنیم یا نه؟

Ping **servername**   :  در پاسخ این پینگ اگر کلاینت با سرورارتباط گرفته باشد آدرس آی پی سرور نمایش داده میشود 

خب بعد از برقراری تست ارتباط , دوباره به ویندوز سرور که اکتیو دایرکتوری روی آن نصب شده بروید. در اینجا ما باید یک USER NAME و پسورد معتبر ایجاد کنیم تا بتوانیم از طریق آن کلاینت را به سرور معرفی کنیم.

در این جا یک user  تعریف میکنیم در سیستم سرور تا بتوانیم با این user  در سیستم کلاینت عضو domain  بشویم.

در سیستم کلاینت از طریق change computer name and change domain  سیستم کلاینت را به دامین خود متصل میکنیم و در این مسیر از ما یوزر و پسور این یوزر تعریف شده را میخواهد. در قسمت دامین باید نام دامین hostname  را وارد کنیم


**شبکه WorkGroup :** شبکه ای است که در آن سیستم اعتبار سنجی متمرکز و امکان استفاده از مکانیسم ها و ابزارهایی بابت اعمال قوانین و تنظمیات مشترک و متمرکز میسر نمیباشد.

در این نوع شبکه هر سیستم پروسه اعتبار سنجی کاربران را به صورت مجزا انجام میدهد

همچنین بابت اعمال تنظیمات مختلف و یکدست نمودن سیستم ها از نظر تنظیمات می بایست تک تک آنها را به صورت مجزا پیکربندی نماییم.



**شبکه Domain :** شبکه ای است که در آن مکانیزم اعتبار سنجی متمرکز وجود دارد ( سرویسی به نام Active Directory ) و نیز امکان اعمال قوانین و  تنظیمات مشترک و متمرکز بر روی همه یا بخشی از سیستم ها وجود دارد.

با راه اندازی سروری به نام Domain controller ، امکان اعتبارسنجی متمرکز و اعمال تنظیمات و پیکربندی به صورت متمرکز در اختیار ما قرار میگیرد.

**Active Directory**:

محصولات ویندوز سرور یعنی همون فایل های شیر شده توی شبکه یا یوزر های ساخته شده توی شبکه یا پرینترهای موجود در شبکه و یا از همه مهمتر دسترسی های موجود در شبکه را اکتیو دایرکتوری به صورت متمرکز درون خودش نگه داری میکند و به صورت تمیز و مرتب در اختیار مدیر شبکه قرار میدهد.

هردامنه برای خود شامل یک یا چندین کنترلر میباشد که یکی از انها درحال اجرا کردن ویندوز سرور میباشد. اکتیودایرکتوری با متمرکز بخشیدن از یک نقطه مدیریت همه ی فعالیت ها را درون شبکه کنترل میکند چون اکتیودایرکتوری یک نقطه ورود واحد برای تمامی منابع شبکه است و مدیر شبکه میتواند تغییرات مربوط درون شبکه را انجام دهد و وارد کامپیوتری بشود و انرا مدیریت کند.اکتیودایرکتوری از سرویس دی ان اس استفاده میکند و میتواند اطلاعات را با هر برنامه کاربردی و یا دایرکتوری مبادله کند.

- **HTTP:**نیز یک پروتوکل استاندارد جهت نمایش صفحات وب میباشد لذا شما میتوانید هر شی داخل مرورگر را به نمایش بگذارید و از فواید اکتیودایرکتوری است که شما میتوانید صفحات وب را با کد HTML به جهت نمایش برای کاربران دراورید. اکتیو دایرکتوری نام های UNC را پشتیبانی میکند نام هایی که در شبکه مبتنی بر ویندوز به درایورهای به اشتراک گذاشته شده و پرینترها و فایل ها مراجعه میکنند.

  عملیات AUTHENTICATION و AUTHORIZATION که عملیات تایید هویت کاربر بعد از زدن رمز عبور و یوزرنیم انجام میشود توسط همین اکتیودایرکتوری صورت میگیرد به این معنا که هنگامیکه سیستم عامل کاربران بالا می آید آنها یوزر نیم و پسورد تعیین شده را وارد کرده و این اطلاعات به سمت سرور اکتیو دایرکتوری مربوط به دامین رفته و در صورت صحیح بودن اطلاعات کاربری اجازه ورود کاربر به سیستم عامل خود را خواهد.

  در اکتیودایرکتوری تمامی دسترسی هایی که به کاربران داده شده است توسط این سرویس اعمال میگردد و هنگام ورود کاربران اعمال میشود به عنوان مثال مدیر شبکه اجازه اجرای برنامه را به شما نداده . این قانون هنگام ورود شما به سیستم بعد از وارد کردن رمز عبور و تایید آن بر روی سیستم شما اعمال میشود.اکتیودایرکتوری دارای دو جز مهم در شبکه میباشد:

1. DNS
1. DHP    


شبکه ی استاندارد مبتنی برACTIVE DIRECTORY شامل موارد زیر است:

1. سرور قدرتمند و استاندارد به همراه سیستم عامل ویندوز سرور
1. ایستگاه های کاری مناسب جهت کار در شبکه با داشتن ویندوزهای مبتنی بر NT
1. شبکه کامپیوتری استاندارد مبتنی بر اصول کابل کشی ساخت یافته
1. پروتکل TCP/IP و همچنین File Sharing در کلیه کامپیوترهای شبکه باید فعال باشند
1. سیستم فایل سرور و در صورت امکان سیستم فایل های ایستگاه های کاری از نوع NTFS باشد
1. در یک شبکه استاندارد آدرس IP سرور معمولا ثابت و دستی انتخاب می شود و ایستگاه های کاری آدرس خود را بطور اتوماتیک از DHCP شبکه دریافت می کنند.
1. DNS زیر ساخت اصلی Active Directory می باشد. این سرویس بطور مستقل و یا در طول نصب Active Directoryقابل نصب می باشد.

**Set IP address for server**

Take care when setting your IP address. Setting it to your most recent IP is actually a bad idea, as it means that address is in the DHCP pool. So technically, you should either pick a number very far out of your DHCP pool, or also edit that pool. Some people like the server at .1, some like it at .254. We recommend setting printers at .200 through .250, routers at .254, servers at .253 and down, and DHCP addresses starting at either 1 or 100.

for instance, a common setup architecture is:
**192.168.1.1** – router
**192.168.1.2** – dns server
**192.168.1.3** – anti-virus firewall
**192.168.1.10** – primary file server
**192.168.1.11** – backup file server
**192.168.1.100** – **200** – workstations (dynamic addresses)
**192.168.1.201** – **254** – printers, phones, fax machines, cameras


### DNS چیست؟
برای درک بهتر سوال **DNS و DNS Server چیست** بهتر است ابتدا تعریفی از DNS (**Domain Name System**) یا **Name Server** یا **سیستم** **نام سرور** ارائه دهیم. DNS (دی ان اس) در واقع یک استاندارد تکنولوژی است که برای مدیریت نام وبسایت‌ها و دامنه‌های موجود در اینترنت و تحت وب استفاده می‌شود. به تعبیری شبیه دفترچه تلفن آنلاینی است که شما را برای اتصال به مخاطب مورد نظرتان هدایت می کند! در دفترچه های تلفن، نام افراد و اطلاعات افراد درج می شود که شما می توانید با جستجوی نام افراد در این دفترچه به اطلاعات مورد نظر آنها دسترسی پیدا کنید! در دنیای وب، زمانی که شما قصد دارید وب سایتی را باز کنید، مرورگرهای اینترنتی با استفاده از DNS ثبت شده بر روی دامنه – در زمان [ثبت دامنه](https://www.irpower.com/services/domain) یا پس از آن – اقدام به پیدا کردن سرور و وب سایت مورد نظر می کنند و از همین طریق می توانند وب سایت درخواست شده را به شما نمایش دهند. برای مثال، شما قصد باز کردن وب سایت [**IRPOWER.com**](https://www.irpower.com/) را دارید که نام دامین را در مرورگر خود تایپ می کنید و Enter را میزنید، بعد از آن مرورگر شما با استفاده از DNS تنظیم شده بر روی نام دامنه مسیر خود را سروری که IRPOWER بر روی آن قرار دارد طی کرده و در نهایت وب سایت را برای شما نمایش می دهد.

DNS Server به سرور کامپیوتری گفته می‌شود که دارای یک دیتابیس از آدرس IPهای عمومی و Hostname های مربوط به آن‌هاست و در اکثر موارد دی‌ان‌اس سرور به عنوان یک تحلیل‌گر (Resolver یا رزولور) یا مترجم نام‌ها به آدرس‌های IP عمل می‌کند.
DNS Server در بستر اینترنت و در حوزه هاستینگ به سیستمی گفته می‌شود که نام دامنه را به IP تبدیل می‌کند. بدین معنا که کاربر آدرس WWW.IRPOWER.COM را در مرورگر وارد می‌کند و سرور دی‌ان‌اس آن را به آی‌پی «176.9.115.11» تبدیل می‌کند. در بسیاری از موارد به DNS Server، سرور دی‌ان‌اس، Name Server و Domain Name System/Server نیز گفته می‌شود.

نحوه کارکرد سرورهای دی‌ان‌اس بر اساس معماری «شبکه client/server» می‌باشد. مرورگر شما به عنوان DNS Client شناخته می‌شود که به آن DNS Resolver نیز گفته می‌شود. به هنگام بازدید وبسایت‌ها، وظیفه این DNS Client ارسال درخواست به سرویس‌دهنده اینترنت شما (ISP شما) می‌باشد.
هر زمان یک DNS Server از سمت یک Client Server مانند مرورگرتان درخواستی دریافت می‌کند که اطلاعات مورد نظر Client Server در دیتابیسش موجود نباشد، خود آن DNS Server نیز نقشش به صورت موقت به DNS Client تغییر می‌کند و از طرف DNS Client اول که مرورگر است، همان درخواست را به سمت DNS Server رده بالاتر خود در این زنجیره و سلسله مراتب ارسال می‌کند. این عمل تا جایی ادامه پیدا می‌کند تا سرانجام در دیتابیس یک DNS Server سطح بالا اطلاعات موجود باشد و در اختیار DNS Client قرار گیرد. پس در این لحظه DNS Server رده بالاتری که اطلاعات IP و نام مورد نظر در دیتابیسش موجود است، آن را به DNS Server سطح پایین‌تر خود می‌دهد و این مورد تا زمان در اختیار قرار گرفتن اطلاعات به DNS Client نخست ادامه پیدا می‌کند.

#### **چرا ما از DNS Server استفاده می‌کنیم**؟
پاسخ این سوال را می‌توان از طریق سوالی دیگر فهمید: حفظ کدام‌یک آسان‌تر است؟ آدرس آی‌پی «176.9.115.11» یا نام WWW.IRPOWER.COM؟ اکثرمان بر این باوریم که حفظ نامی مانند IRPOWER از تعدادی عدد بدون ترتیب آسان‌تر است.
پس وقتی می‌خواهیم به یک وبسایت مانند IRPOWER مراجعه کنیم، تنها آدرس WWW.IRPOWER.COM را در مرورگر وارد می‌کنم و تنها چیزی که لازم است به خاطرمان بسپاریم نام IRPOWER است. این مورد برای وبسایت‌های دیگر مانند Google.com نیز صادق است.
عکس این مورد نیز درست است. یعنی ما به عنوان یک انسان کلمات یک URL را می‌فهمیم و آن را بسیار راحت‌تر از آی‌پی به خاطر می‌سپاریم اما کامپیوتر‌ها و دستگاه‌های متصل به شبکه آدرس IP را متوجه می‌شوند.
بنابراین برای دسترسی به وبسایت‌ها از DNS Server استفاده می‌کنیم نه تنها به این دلیل که تنها میخواهیم از نام‌های آسان قابل فهم برای انسان استفاده کنیم بلکه به این دلیل که کامپیوترها برای دسترسی به وبسایت‌ها نیاز به استفاده از آدرس IP دارند. در این مابین سرور دی‌ان‌اس به عنوان مترجمی بین دامنه و IP عمل می‌کند.

#### **DNS Serverها و بدافزارها**
استفاده از آنتی‌ویروسی قدرمتند بسیار مهم است. یکی از دلایل آن این است که بدافزار می‌تواند به سیستم شما حمله کرده و تنظیمات مربوط به دی‌ان‌اس سرورها را تغییر دهد. برای مثال فرض کنید کامپیوتر شما در حال استفاده از سرورهای دی‌ان‌اس گوگل به آدرس 8.8.8.8 و 8.8.4.4 است. تحت این دی‌ان‌اس سرورها، با وارد کردن آدرس وبسایت بانک مورد استفاده‌تان، به صفحه مورد نظر دسترسی پیدا می‌کنید و عملیات بانکی را با موفقیت انجام می‌دهید.حال فرض کنید بدافزاری تنظیمات **DNS Server** شما را تغییر داده باشد (که این عمل می‌تواند به صورت پنهانی و بدون آگاهی شما اتفاق افتد). در این شرایط با وارد نمودن همان آدرس وبسایت بانک ممکن است به صفحه‌ای متمایز و بی‌ربط ارجاع داده شوید و حتی مهم‌تر از آن به وبسایتی ارجاع داده شوید که کاملاً شبیه به وبسایت بانکتان است؛ در صورتی که اینگونه نیست. این وبسایت تقلبی شاید کاملاً شبیه به وبسایت اصلی بانک باشد اما پس از وارد نمودن اطلاعات ورود به حساب بانکی، به جای وارد شدن به اکانت بانکیتان، تنها اطلاعات ورود شما را ضبط کرده و می‌رباید.

دو راه برای پیشگیری از قربانی شدن به این روش وجود دارد. راه اول نصب آنتی‌ویروسی قدرتمند است که بوسیله آن بدافزارها پیش از آسیب رساندن به سیستم یافته و حذف شوند و دوم آگاهی از نحوه نمایش و عملکرد وبسایت است. معمولاً ظاهر وبسایت‌ پس از ورود به نسخه‌ی جعلی آن دقیقاً مشابه مورد اصلی آن نیست و حتی ممکن است اخطاری با مضمون «Invalid Certificate» یا موارد مشابه دریافت کنید که می‌تواند حاکی از ورود به وبسایتی ساختگی داشته باشد.

` `اگر دی‌ان‌اس سرورهای ISP شما از دی‌ان‌اس سرورهای Google نزدیک‌تر باشد، سرعت دسترسی به وبسایت‌ها و یا تحلیل (Resolve) آدرس‌های اینترنتی سریع‌تر از دی‌ان‌اس‌های گوگل انجام می‌شود. عکس این مورد نیز صحیح است.
چنانچه تجربه قطعی و مشکلات شبکه دارید به طوری که محتوای هیچ وبسایتی نمایش داده نشود، ممکن است این مشکل از DNS Serverها نشأت گرفته باشد. در صورتی که دی‌ان‌اس سرور نتواند IP مربوط به Hostname یا دامنه‌ای که وارد می‌کنید را پیدا کند، وبسایت بارگذاری نمی‌شود و عملاً دسترسی به آن نخواهید داشت. زیرا کامپیوترها از طریق IP با یکدیگر ارتباط برقرار می‌کنند.

دستور **nslookup** برای استعلام دی‌ان‌اس سرور تنظیم شده مورد استفاده قرار می‌گیرد. 

**What is 127.0.0.1?**

**127.0.0.1** is known as a loopback address, but you may see it under the name "**localhost**." When you point your browser to 127.0.0.1, it tries to connect to the computer you're using right now. This is handy when you want to connect to a server on your own computer.

127\.0.0.1 is special among IP addresses. Typically, an IP address is unique to every computer on both your local network and the internet. 127.0.0.1, however, always points to the computer you're currently using no matter what.

For example, if you set up a server on Computer A, you can connect to it by visiting 127.0.0.1 on Computer A. However, if you move to Computer B and type in 127.0.0.1, you'll connect to Computer B instead of A. You'll need either Computer A's internet or local network IP address to connect to it from Computer B.

While 127.0.0.1 doesn't do much by itself, things change when you run a server on your computer. When you do, your computer now has a reason to listen to incoming connections, so it won't refuse your request.

For example, let's say you're setting up a server that you want others to connect to in the future. Regardless of if you're using premade software or you're coding the server yourself, you may want to give it a "test run" to ensure it works before letting others connect.

To do this, you can run the server on your computer, then connect to it using 127.0.0.1. The server will load in your browser as if you had connected to it via the internet while also barring anyone else from peeking in on your work-in-progress.

ضمنا روی کارت شبکه کلاینت ها و همچنین سرور ها آدرس DNS سرور داخلی (دامین کنترلر) رو وارد کنید و از ست کردن آدرس های Public DNS هایی مثل **۸.۸.۸.۸** خودداری کنید. 

توی کارت شبکه DNS Server هم Preferred DNS server رو 127.0.0.1 ست نکنید. اگه DC های دیگه ای توی شبکه دارید ( که ظاهرا آدرسش 192.168.1.72 هست ) آدرس IP اونو ست کنید. در قسمت Alternate DNS server هم 127.0.0.1 رو ست کنید. توی DC بعدی هم DNS اول رو 192.168.1.70 و DNS دوم رو 127.0.0.1 ست کنید..

**Default geteway / DNS server**

A default gateway is the host that your server will use when trying to connect to anything that's not on the same network as it is. A default gateway is the interface address of a router and a router's job is to intercommunicate different IP networks. The default gateway works as a gateway for IP address of a network to communicate with the IP address of another IP network.

**DNS** resolves **domain name** such as Google.com into IP address such as 202.22.22.22. Normally there are two types of DNS resolution, **Internal DNS and External DNS**. Internal DNS works for internal Domain name resolution such as if we have multiple domain entries using windows Server, windows server will resolve those entries locally as those servers are present on same network.

However when we browse the Internet, we need external DNS resolution, for which we must know that how can we reach or communicate to external DNS which is actually IP address of a different network. Now we need router to route our packet from internal network to external network for domain name resolution. now we send our packet to router interface which is our gateway address, router routes our packet to the DNS server IP address where our DNS request gets resolved and comes back same route of default gateway.

**Nslookup   :**

` `**nslookup** is a simple but very practical command-line tool, which is principally used to find the IP address that corresponds to a host, or the domain name that corresponds to an IP address (a process called “Reverse DNS Lookup”)**.**

**Ping :**

A ping is a signal sent to a [host](https://techterms.com/definition/host) that requests a response. It serves two primary purposes: 1) to check if the host is available and 2) to measure how long the response takes. To perform a ping command from a command line interface, simply type "ping" followed by the IP address or domain name of the host you want to ping.

1. **< 30 ms** - excellent ping; almost unnoticeable; ideal for online gaming
1. **30 to 50 ms** - average ping; still ok for online gaming
1. **50 to 100 ms** - somewhat slow ping time; not too noticeable for web browsing but may affect gaming
1. **100 ms to 500 ms** - slow ping; minimal effect on web browsing, but will create noticeable [lag](https://techterms.com/definition/lag) in online gaming










