# Investigacion

# SMS

Para poder integrar SMS a nuestro proyecto, usaremos Twilio.

Para efectos de la investigación, el demo está hecho en .NET Framework console application.

--Abrimos el Package Manager Console en Visual Studio

>> Install-Package Twilio

Una vez que está instalado Twilio

En el program.cs agregamos las dependencias correspondientes

>> using Twilio

>> using Twilio.Rest.Api.V2010.Account

>> using Twilio.Types

Tenemos que crearnos una cuenta en TWILIO y generar un numero de telefono.

>> Se te da un free-trial donde tienes un balance de $15.50 para probar los servicios y ahí mismo puedes acceder a un trial phone number, que lo necesitarás para implementar los SMS en el proyecto. (todos los pasos son continuos desde que le clickeas sign up)

Una vez con la cuenta creada y el phone number creado, debemos inicializar el cliente.

# Inicializacion del cliente

Inicializar el cliente para futuras llamadas a la API REST ahora es un método estático. Para la mayoría de los casos de uso, no es necesario crear directamente un objeto de cliente. Este paso lo vamos a hacer en el Program.cs

Las variables del ambiente las vamos a inicializar de la siguiente manera: 

este es el account Id de tu cuenta de Twilio, en este caso estamos usando los TEST CREDENTIALS
>> string accountSid = "TWILIO_ACCOUNT_SID";

este es el authToken de tu cuenta de Twilio, en este caso estamos usando los TEST CREDENTIALS
>> string authToken = "TWILIO_auth_token";

Luego se utilizan ambas credenciales para inicializar el TWILIO REST client object.

esto inicializa el REST client con las credenciales
>> TwilioClient.Init(accountSid, authToken);

Esto solo debe hacerse una vez. Todas las llamadas posteriores a la API Twilio se autentican utilizando las credenciales pasadas al método Init.

Necesitamos un número remitente, para enviar un mensaje de texto y un número destinatario, que lo recibe. Asimismo, como un mensaje de texto.

https://www.twilio.com/docs/iam/test-credentials se puede ver mas informacion de como usar los test credentials

este es el telefono a mandar el SMS, pero no tenemos como probar con un # en CR con el free trial, por lo que es un dummy number
>> var to = new PhoneNumber("+15555551234");
  
este es el telefono que manda el SMS, pero no tenemos como probar con un # en CR con el free trial, por lo que es un dummy numberb
>> var from = new PhoneNumber("+12562903696");

aca creas el SMS, podes destinatario, remitente y el texto a enviar
>> var message =MessageResource.Create(
>>    to: to,
>>    from: from,
>>    body: "Yaaay, nuestro primer mensaje de texto usando C#!"
>> );

y para finalizar, como no podemos probar con numeros reales, haremos un print del ID del SMS para confirmar que si fue enviado y el contenido del mensaje
>>      Console.Write(message.Sid);
>>      Console.Write("    ");
>>      Console.Write(message.Body);
>>      Console.ReadLine();

El video del DEMO de SMS puede ser encontrado en el siguiente link https://drive.google.com/file/d/1DAvBLlV64FMgbCM9H_JXUKbAnEIFc8sA/view?usp=sharing o directamente en el repositorio como un MP4
