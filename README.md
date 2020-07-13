# Investigacion

# SMS

Para poder integrar SMS a nuestro proyecto, usaremos Twilio.

Para efectos de la investigación, el demo está hecho en .NET Framework console application.

--Abrimos el Package Manager Console en Visual Studio

>> Install-Package Twilio

Una vez que está instalado Twilio

En el program.cs agregamos las dependencias correspondientes

using Twilio;
using Twilio.Rest.Api.V2010.Account;
using Twilio.Types;

Tenemos que crearnos una cuenta en TWILIO y generar un numero de telefono.

>> Se te da un free-trial donde tienes un balance de $15.50 para probar los servicios y ahí mismo puedes acceder a un trial phone number, que lo necesitarás para implementar los SMS en el proyecto.

Ahora debemos inicializar el cliente.

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

https://www.twilio.com/docs/iam/test-credentials se puede ver mas informacion de como usar los test credentials aca

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

# SendGrid

SendGrid es una plataforma de omunicación basada en el cliente, exclusive para correos eletrónicos transacionales y de mercadeo. La compañía prove un servicio basado en la nube, que asiste a las empresas con el envío de correo electrónico.

El servicio administra varios tipos de correo electrónico, que incluyen notificaciones de envío, solicitudes de Amistad, confirmaciones de registro y boletines informativos (o “news letters”). Además, se ofrecen servicios de rastreo de hipervínculos, y reportes que permiten a las compañías que contratan sus servicios trazar la cantidad de correos electrónicos abiertos, retiros de subscripciones, correos electrónicos “rebotados” o enviados a una dirección inactive, y reportes de correo no deseado o spam. Desde el 2012, se han integrado servicios de envío de SMS, mensajes de voz y notificaciones de inserción, al asociarse con la compañía Twilio.

Sus características permiten que los desarrolladores de software y especialistas de mercadeo la utilicen para crear, segmentar, probar y enviar correos electrónicos para casos de uso como confirmación de compras, instrucciones para la reinstauración de contraseña, ventas u ofertas disponibles en el future, campañas de diversas índoles, etc.
Los anuncios se realizan mediante una architectura completamente redundante, que alcanza enviar aproximadamente 60 billones de correos electrónico mensualmente. Las notificaciones se fealizan mediante APIs RESTul y librerías que soportan la mayoría de los enguajes de programación existentes actualmente. Todo esto permite la colaboración entre diferentes equipos de trabajo para diseñar los correos electrónicos, notificaciones y machotes para crear y examinr el contenido.

La integración con los APIse realiza en pocos minutos, gracias a la documentación para crear las instrucciones para la restauración de contraseñas, enviar mensajes de mercadeo y personalizar las experiencias que los clientes apreciarán.
Ejemplo de la integración utilizanco C#:
 
>>  // using SendGrid's C# Library
>>  // https://github.com/sendgrid/sendgrid-csharp
>>  using SendGrid;
>>  using SendGrid.Helpers.Mail;
>>  using System;
>>  using System.Threading.Tasks;

>>  namespace Example
>>  {
>>      internal class Example
>>      {
>>          private static void Main()
>>          {
>>              Execute().Wait();
>>          }
>>  
>>          static async Task Execute()
>>          {
>>              var apiKey = Environment.GetEnvironmentVariable("NAME_OF_THE_ENVIRONMENT_VARIABLE_FOR_YOUR_SENDGRID_KEY");
>>              var client = new SendGridClient(apiKey);
>>              var from = new EmailAddress("test@example.com", "Example User");
>>              var subject = "Sending with SendGrid is Fun";
>>              var to = new EmailAddress("test@example.com", "Example User");
>>              var plainTextContent = "and easy to do anywhere, even with C#";
>>              var htmlContent = "<strong>and easy to do anywhere, even with C#</strong>";
>>              var msg = MailHelper.CreateSingleEmail(from, to, subject, plainTextContent, htmlContent);
>>              var response = await client.SendEmailAsync(msg);
>>          }
>>      }
>>  }

# Como instalarlo?
# Prerrequisitos 
.NET 4.5.2 o mayor.
.NET Core 1.0 o mayor.
.NET Standard 1.3 (support).
# Instrucciones
Se debe tener una cuenta Twilio SendGrid, que es gratis para enviar hasta 40 000 correos electrónicos por día durante los primeros 30 días. Posteriormente, se pueden enviar 100 correos electrónicos por día.
Obtener el API Key, desde la cuenta de Twilio SendGrid.
Agregar el API Key a los environment variables.
Crear el proyecto en Visual Studio - .NET Console App.
Agregarle el NuGet de Sengrid Install.
En Program.cs, utilizar código anterior haciendo las modificaciones correspondientes.
Correrlo desde Visual Studio.
Listo! Verificar que el correo haya llegado a la dirección indicada.

# Video explicativo
https://drive.google.com/file/d/1WFn6_rKscO-waut3z0-A1l62fJQUmxoV/view?usp=sharing

Otras páginas de referencia:
• https://en.wikipedia.org/wiki/SendGrid
• https://craft.co/sendgrid
• https://www.twilio.com/sendgrid/email-api
• https://github.com/sendgrid/sendgrid-csharp#quick-start 


# HTMLTOPDF
Link: https://selectpdf.com/html-to-pdf/demo/

SelectPdf Html To Pdf Converter for .NET  es un componente poderoso que permite generar documentos de pdf directamente de páginas web y código HTML en ambientes de trabajo .NET
Este componente no tiene dependencias de terceros y no necesita que los usuarios instalen Adobe para tener la capacidad de crear documentos en PDF.

Importante
La edición para la comunidad de “Selectpf” no es una prueba de prueba gratuita para la librería comercial.
Este es un producto gratuito con funcionalidad limitada, en caso de querer utilizar todas las funcionalidades este seria el link para una muestra de prueba http://selectpdf.com/pdf-library-for-net/
Las siguientes caracteristicas no son parte de la versión gratuita de la comunidad, si se desean utilizar se debe de adquirir la versión completa comercial en el siguiente link : SelectPdf Library for .NET

	Crear documentos en PDF de más de 5 paginas
	Convertir solo cierta sección de la página, especificando el elemento de ID
	Iniciar manualmente la conversión a pdf desde javascript
	Especificar un script de JS que se ejecute antes de la conversión
	Ocultar partes de la pagina web durante la conversión de HTML a PDF
	Cargar y modificar documentos existentes de PDF 
	Agregar HTML adicionales, textos,imágenes a pdf ( usando los objetos PdfHtmlElement, PdfTextElement, PdfImageElement)
	Obtener la localización de los elementos web en el pdf
	Especificar la acción de apertura del documento de PDF (brincar de página, correr script)
	Modificar encabezados y pies de pagina en la paginas de los PDF
	Permitir campos de relleno en los PDF
	Extraer texto del PDF(PDF a convertidor de texto)
	Modificar el tamaño del contenido en los documentos de PDF
	Buscar por texto en el PDF
	Convertir paginas de PDF en imágenes


Que permite la versión de comunidad gratuita
	Convertir documentos a pdf hasta de 5 paginas
	Convertir cual pagina web a PDF
	Convertir cual raw html string a PDF
	Definir las opciones de la pagina de PDF
	Definir propiedades del documento 
	Definir preferencias de vista
	Definir seguridad del pdf

Como instalar.
La forma mas sencilla de instalar SelectPdf Html to Pdf Converter es usando la instalación mediante paquete de Nuger, 

Creas tu Proyecto, luego vas al Nuget Package manager y instalas uno de los siguientes paquetes:

NET Framework version - AnyCPU (.NET 2.0 and .NET 4.0-4.5) - Select.HtmlToPdf: https://www.nuget.org/packages/Select.HtmlToPdf/.

.NET Core version - Windows only (and .NET 4.6.1 and .NET 4.7.2) - Select.HtmlToPdf.NetCore: https://www.nuget.org/packages/Select.HtmlToPdf.NetCore/.

.NET Core version with Blink rendering engine - Windows only (and .NET 4.6.1 and .NET 4.7.2)- Select.HtmlToPdf.NetCore.Blink: https://www.nuget.org/packages/Select.HtmlToPdf.NetCore.Blink/.

Note: The .NET Core version is for .NET Core 2.0 or above through .NET Standard 2.0. Currently it requires a Windows system to run. It does not work on Linux or Mac or Xamarin.
Note 2: Blink rendering engine only works with .NET Core version and with .NET Framework starting with 4.6.1. Blink rendering engine was introduced with SelectPdf v19.1.

Video basado en la explicacion: https://www.youtube.com/watch?v=_ycJtgKDZEY


