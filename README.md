## Integrating MOLPay API with ASP.NET
Version 1.0.0

### Pre-Requisite
1. Visual Studio 2012 or above.
2. MOLPay Development or Production ID.
3. MOLPay General API

### Installation

#### Via File Explorer
1. Download `MOLPay.API.dll` library.
2. Open Visual Studio project, right click on your project name in `Solution Explorer` and choose `Add Reference`.
3. Click `Browse` to search for downloaded library. Click `OK` to add.

#### Via NuGet Package Manager
1. Open `Package Manager Console` in Visual Studio.
2. On console, type in `Install-Package MOLPay.API` command.

### Usage
Import `MOLPay` library at any of project code file.

```C#
using MOLPay
```

To create object for preferred request, you might want to use below class:

| API Function        | Class Name |
| ------------- |:-------------:| 
| Seamless Payment     | Seamless | 
| Recurring Payment    | Recurring |   
| Payment Status Query | PSQ  |
| Reversal Request | Reversal |
| Capture Transaction | Capture |

For example, to create Seamless Integration object, will look like this:
```C#
Seamless payment = new Seamless()
```

#### MOLPay Seamless Integration (Seamless)
To send payment request using [Seamless Integration](https://github.com/MOLPay/Seamless_Integration) you may create object from `Seamless` class.

```C#
Seamless payment = new Seamless();
payment.status = true;
payment.mpsmerchantid = "merchantid";
payment.vkey = "eaf961b86c05a45ab87041d6389dff55";
payment.mpschannel = context.Request["payment_options"];
payment.mpsamount = context.Request["total_amount"]);
payment.mpsorderid = context.Request["orderid"];
payment.mpsbill_name = context.Request["billingFirstName"] + " " + context.Request["billingLastName"];
payment.mpsbill_mobile = context.Request["billingMobile"];
payment.mpsbill_email = context.Request["billingEmail"];
payment.mpsbill_desc = context.Request["billingAddress"];
payment.mpscountry = context.Request["country"];
payment.mpscurrency = context.Request["currency"];
payment.mpslangcode = "en";
payment.mpstcctype = "SALS";

//This part to JSON Encode using JSON.NET
string str = JsonConvert.SerializeObject(payment);
context.Response.ContentType = "text/json";
context.Response.Write(str);
```

### Support or Contact
This is NOT official library from MOLPay. Therefore, no official support will be given to you. Please use this library as a guideline to integrate MOLPay service with ASP.NET project. If there is any dispute between this document and official MOLPay release, please use the MOLPay version. 

You also understand that you accept the risk and no other party will be held liable for any loss or damage cause by the usage of any information obtained in this page or software library.


### Changelog
2017-02-25 - v1.0.0 - Initial Release with Seamless Integration 
