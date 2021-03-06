## Integrating MOLPay with ASP.NET
Version 1.0.1

### Pre-Requisite
1. Visual Studio 2012 or above.
2. MOLPay Development or Production ID.
3. MOLPay General API.

### Installation

#### Via File Explorer
1. Download `MOLPay.dll` library.
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
| Seamless Integration     | Seamless | 
| Recurring Payment    | Recurring |   
| MassPayment Profile | MassPayment |

For example, to create Seamless Integration object, will look like this:
```C#
Seamless payment = new Seamless()
```

#### Seamless Integration
Code snippet for payment request using [Seamless Integration](https://github.com/MOLPay/Seamless_Integration). You may create object from `Seamless` class.

```C#
Seamless payment = new Seamless();
payment.status = true;
payment.mpsmerchantid = "___MERCHANTID___";
payment.vkey = "___VERIFYKEY___";
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
context.Response.ContentType = "application/json";
context.Response.Write(str);
```

#### Recurring Payment
Code snippet for recurring payment instruction. You may create object from `Recurring` class.

```C#
NameValueCollection param = new NameValueCollection();
Recurring record = new Recurring();
        
record.recordtype = "T";
record.merchantid = "___MERCHANT___";
record.verifykey = "___VERIFYKEY___";
record.token = "___TOKEN___";
record.orderid = "___ORDERID___";
record.amount = ___AMOUNT___;        
param.Add(i.ToString(), record.GetInstruction());
        
using (WebClient client = new WebClient()) {
  resp = client.UploadValues("https://www.onlinepayment.com.my/MOLPay/API/Recurring/input.php", param);
  context.Response.ContentType = "application/json";
  context.Response.Write(System.Text.Encoding.UTF8.GetString(resp));
}
```
#### Mass Payment Profile
Code snippet for creating mass payment profile. You may create object from `MassPayment` class.
```C#
MassPayment Data = new MassPayment();
MassPayment.PayeeProfile Person = new MassPayment.PayeeProfile();

Person.Full_Name = "NUR FATHIA BINTI HASSAN";
Person.Type = "Individual";
Person.NRIC_Passport = "920321022468";
Person.Country = "MY";
Person.Bank_Code = "CIBBMYKL";
Person.Bank_AccName = Person.Full_Name; // Match Full Name
Person.Bank_AccNumber = "12345678";
Person.Email = "fathia@gmail.com";
Person.Mobile = "0123456781";
            
Data.Operator = "___MERCHANT___";
Data.verifykey = "___VERIFYKEY___";
Data.Func = "new";
Data.Profile = Person;
Data.Profilehash = "12345678";

using (WebClient client = new WebClient()) {
   NameValueCollection param = new NameValueCollection();
   param.Add(Data.GetInstruction());
   resp = client.UploadValues("https://www.onlinepayment.com.my/MOLPay/API/MassPayment/payee_profile.php", param);
   context.Response.ContentType = "application/json";
   context.Response.Write(System.Text.Encoding.UTF8.GetString(resp));
}
```

### Support or Contact
This is NOT official library from MOLPay. Therefore, no official support will be given to you. Please use this library as a guideline to integrate MOLPay service with ASP.NET project. If there is any dispute between this document and official MOLPay release, please use the MOLPay version. 

You also understand that you accept the risk and no other party will be held liable for any loss or damage cause by the usage of any information obtained in this page or software library.


### Changelog
1. 2017-02-26 - v1.0.1 - Bug Fix
2. 2017-02-25 - v1.0.0 - Initial Release
