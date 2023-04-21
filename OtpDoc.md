# Fingo Gateway Otp Api

**Fingo Otp** Es un api que provee la funcionalidad de envio de Otp, mensajes de correo y Sms personalizados previamente

## Operaciones

 - [SendOtp](#ApiSendOtp)
 - [ValidateOtp](#ApiValidateOtp)
 - [SendMailFormStatus](#ApiSendMailFormStatus)
 - [SendMailFinkeeperStatus](#ApiSendMailFinkeeperStatus)

**Fingo Gateway**  es un servicio comercial, para su uso, contacte a  [info@bytte.com.co](mailto:info@bytte.com.co) para obtener instrucciones y credenciales de acceso

**FinGo y MiiD** Son Marcas registradas por Bytte S.A.S 

## Detalle de Operaciones:
## <a name="SendOtp"></a>SendOtp

Operación encargada de la generacion y envio de Otp por medio de Mensaje Sms y Correo electronico

Url **POST** https://servicesdev.fingo.credit/otp/api/SendOtp/

```json
{
    "userName": "Allan Diaz",
    "emailAddress": "allan.diaz@bytte.com.co",
    "countryCode": "57",
    "phoneNumber": "3016336165"
}
```

Variables a enviar:
* **userName** = Nombre del Usuario personalizado Ej: **"Pedro Perez"**
* **emailAddress** : Direccion de correo donde será enviado el Otp
* **countryCode** : Código del pais donde se enviará el Otp a dispositivo movil
* **phoneNumber** : Número de telefono donde se enviará el Otp a dispositivo movil

Si la informacion ingresada es correcta, el Api Retorna
* **status** : 200

```json
{
    "validationKey": "00b90bcf-843d-48f9-967a-9ae79d0146ff",
    "isValid": true
}
```

Variables de respuesta:
* **validationKey** : Identificador dela Otp que se validara
* **isValid** : *Bandera donde se puede evaluar si la operacion es valida o no*

---
## <a name="ApiValidateOtp"></a>Validate Otp
Valida la información de la Otp

Url - **POST** https://servicesdev.fingo.credit/otp/api/ValidateOtp/ 

Body
```json
{
    "emailAddress": "allan.diaz@bytte.com.co",
    "validationKey": "00b90bcf-843d-48f9-967a-9ae79d0146ff",
    "code": "214680"
}
```
Variables a enviar:
* **emailAddress** : Direccion de correo donde fué enviado el Otp
* **validationKey** : Identificador dela Otp que se validara
* **code** : Codigo Otp ingresado por el usuario

Si la informacion ingresada es correcta, el Api Retorna
* **status** : 200

```json
{
    "isValid": true,
    "message": "Valid Code"
}
```

Variables de respuesta:
* **message** : Descripción de la Validacion de la Otp
* **isValid** : *Bandera donde se puede evaluar si el Otp es Valido o no*
---

## <a name="ApiSendMailFormStatus"></a>SendMailFormStatus
Operación encargada del envio de correo de Status del proceso.

El Mensaje a enviar Tiene el siguiente formato

---
Hola!

**(username)**!, ha iniciado una solicitud de crédito en línea con fingo, se encuentra en **(status)**, a continuación se relaciona código de formulario: 

Código de formulario: **(formId)**.

Con este código podrá realizar seguimiento a su solicitud en nuestra página web: **(urlWebSite)**
fingo.co 

---

Url - **POST** https://servicesdev.fingo.credit/otp/api/SendMailFormStatus/

Body
```json
{
    "emailAddress": "allan.diaz@bytte.com.co",
    "countryCode": "57",
    "phoneNumber": "3016336165",
    "userName": "Allan Diaz",
    "status": "RECHAZADA",
    "formId": "ABC-12345",
    "urlWebSite": "https://form.fingo.co/"
}
```

Variables a enviar:
* **userName** = Nombre del Usuario personalizado Ej: **"Pedro Perez"**
* **emailAddress** : Direccion de correo donde será enviado el Otp
* **countryCode** : Código del pais donde se enviará el Otp a dispositivo movil
* **phoneNumber** : Número de telefono donde se enviará el Otp a dispositivo movil
* **status** : Estado de la Solicitud
* **formId** : Identificador de la Solicitud
* **urlWebSite** : Url Web Site de retoma

Si la informacion ingresada es correcta, el Api Retorna
* **status** : 200

```json
{
    "isValid": true
}
```

Variables de respuesta:
* **isValid** : *Bandera donde se puede evaluar si el envio es o no correcto*

---
## <a name="ApiSendMailFinkeeperStatus"></a>SendMailFinkeeperStatus
Operación encargada del envio de correo de notificacion para el Sistema **Finkeeper**.

El Mensaje a enviar Tiene el siguiente formato

---
Hola!

El análisis de información realizada por **(operator)** para la empresa 
**(company)** ha sido **(status)**, para realizar seguimiento al estado de la solicitud, 
se relaciona código de verificación y página web 

Código solicitud crédito: **(formId)**.
finkeeper.fingo.co 
**(urlWebSite)**
fingo.co 

---
Url - **POST** https://servicesdev.fingo.credit/otp/api/SendMailFinkeeperStatus

Body
```json
{
    "emailAddress": "allan.diaz@bytte.com.co", 
    "company": "Lavanderia la quebrada S.A.S",
    "status": "RECHAZADA",
    "formId": "ABC-12345",
    "urlWebSite": "https://finkeeper.fingo.co/",
    "operator": "operador123@bytte.com.co"
}
```

Variables a enviar:
* **company** = Nombre de la empresa en proceso
* **emailAddress** : Direccion de correo donde será enviado el Otp
* **operator** : Nombre/Correo del operador en FinKeeper que realizo la operacion
* **status** : Estado de la Solicitud
* **formId** : Identificador de la Solicitud
* **urlWebSite** : Url Web Site de Sitio FinKeeper

Si la informacion ingresada es correcta, el Api Retorna
* **status** : 200

```json
{
    "isValid": true
}
```

Variables de respuesta:
* **isValid** : *Bandera donde se puede evaluar si el envio es o no correcto*
---
