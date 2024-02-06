---
description: Using SDK to validate format of each field
---

# Pagsmile SDK

### Parameter Validation

| Merhod                         | Arg1                                                                             | Arg2                                                                                            | Result                                          | Note                                                                                      |
| ------------------------------ | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------- | ----------------------------------------------------------------------------------------- |
| formatId(value, code)          | (string) Id to be formatted                                                      | (string) ISO 3166, 3 digit country code (MEX, CHL, COL, PER, ECU, BRA, PAN, CRI, SLV, GTM, NIC) | (string) formatted id                           | IDs can beformatted: (CPF/CNPJ, RFC, NIT/CC, RUT/RUN, DNI/RUC, RUC, CIP, DUI, DPI)        |
| validateId(value, code)        | (string) Id to be validated                                                      | (string) ISO 3166, 3 digit country code (MEX, CHL, COL, PER, ECU, BRA, PAN, CRI, SLV, GTM, NIC) | (list) \[isIdvalid (boolean), idType (string) ] | IDs can bevalidated: CPF/CNPJ, RFC, NIT/CC, RUT/RUN, DNI/RUC, RUC, CIP, DUI, DPI          |
| validateName(value)            | (string) name to be validated                                                    | -                                                                                               |                                                 | Only canbeused in MEX, CHL, COL, PER, ECU, BRA, PAN, CRI, SLV, GTM, NIC                   |
| validateEmail(value)           | (string) email to be validated                                                   | -                                                                                               | (boolean) true/false                            |                                                                                           |
| formatCEP(value)               | (string) CEP (zip code) to be formatted                                          | -                                                                                               | (string) formatted CEP (zip code)               |                                                                                           |
| validateCEP(value)             | (string) CEP to be validated                                                     | -                                                                                               | (boolean) true/false                            |                                                                                           |
| pagsmileDocNumclearData(value) | (string) Data to be cleared in order to get rid of unnecessary characters (-/.). | -                                                                                               | (string) cleared data                           | <mark style="color:red;">Before theAPI request formattedparameters must be cleared</mark> |

**Step 1: Import below library by adding between tag in your code.**

```
<script type="text/javascript" src="https://checkout.pagsmile.com/public/pagsmileSDK/outboundlibs/pagsmileSDK.min.js"></script>
```

**Step 2: Call above listed methods using pagsmileSDK.**

Example:

```
pagsmileSDK.formatId("50284414727","BRA") // 502.844.147-27
pagsmileSDK.validateId("502.844.147-27", "BRA") // [true, 'CPF']
pagsmileSDK.clearData("502.844.147-27") // 50284414727
```

### Demo Website <a href="#monitor-form-submission-events" id="monitor-form-submission-events"></a>

Click [here ](https://checkout.pagsmile.com/public/pagsmileSDK/sdkExample.html)to access demo website.

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Example</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script type="text/javascript" src="https://checkout.pagsmile.com/public/pagsmileSDK/outboundlibs/pagsmileSDK.min.js"></script>
    <style type="text/css">
      .error {
        border-color: red;
      }
    </style>
  </head>
  <body>
    <label for="">RFC: </label>
    <input type="text" id="input-rfc" /> <button id="submit-mx-id">Submit RFC</button>
    <br />

    <br />
    <label for="">CPF/CNPJ: </label>
    <input type="text" id="input-br-id" /> <button id="submit-br-id">Submit CPF/CNPJ</button>
    <br />

    <br />
    <label for="">CEP: </label>
    <input type="text" id="input-cep" /> <button id="submit-cep">Submit CEP</button>
    <br />

    <script type="text/javascript" charset="utf-8">
      $("#input-rfc").on("input", (e) => {
        const value = e.target.value;
        const idNode = $("#input-rfc");

        const formattedId = pagsmileSDK.formatId(value, "MEX");
        idNode.val(formattedId);

        const [isIdvalid, idType] = pagsmileSDK.validateId(idNode.val(), "MEX");

        if (isIdvalid) {
          idNode.removeClass("error");
        } else {
          idNode.addClass("error");
        }
      });
      $("#submit-mx-id").click(() => {
        const idNode = $("#input-rfc");
        const [isIdvalid, idType] = pagsmileSDK.validateId(idNode.val(), "MEX");
        if (isIdvalid) {
          const requestData = {
            customer: {
              identify: {
                number: pagsmileSDK.clearData(idNode.val()),
                type: idType,
              }, // .....
            },
          };

          window.alert(JSON.stringify(requestData));
        }
      });

      $("#input-br-id").on("input", (e) => {
        const value = e.target.value;
        const idNode = $("#input-br-id");

        const formattedId = pagsmileSDK.formatId(value, "BRA");
        idNode.val(formattedId);

        const [isIdvalid, idType] = pagsmileSDK.validateId(idNode.val(), "BRA");
        if (isIdvalid) {
          idNode.removeClass("error");
        } else {
          idNode.addClass("error");
        }
      });
      $("#submit-br-id").click(() => {
        const idNode = $("#input-br-id");
        const [isIdvalid, idType] = pagsmileSDK.validateId(idNode.val(), "BRA");
        if (isIdvalid) {
          const requestData = {
            customer: {
              identify: {
                number: pagsmileSDK.clearData(idNode.val()),
                type: idType,
              }, // .....
            },
          };

          window.alert(JSON.stringify(requestData));
        }
      });

      $("#input-cep").on("input", (e) => {
        const value = e.target.value;
        const cepNode = $("#input-cep");

        const formattedCep = pagsmileSDK.formatCEP(value);
        cepNode.val(formattedCep);

        const isCepValid = pagsmileSDK.validateCEP(cepNode.val());
        if (isCepValid) {
          cepNode.removeClass("error");
        } else {
          cepNode.addClass("error");
        }
      });
      $("#submit-cep").click(() => {
        const cepNode = $("#input-cep");
        const isCepValid = pagsmileSDK.validateCEP(cepNode.val());
        if (isCepValid) {
          const requestData = {
            customer: {
              address: {
                zip_code: pagsmileSDK.clearData(cepNode.val()),
              },
            },
          };

          window.alert(JSON.stringify(requestData));
        }
      });
    </script>
  </body>
</html>

```
