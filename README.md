# RFC-Consulta-API

[Read this README in English](README_eng.md)

## Descripción
Este repositorio proporciona una API REST fácil de usar para consultar información del RFC (Registro Federal de Contribuyentes) en México.

## Instrucciones de Uso
Por el momento, la API es accesible desde cualquier dispositivo con acceso a Internet. La API se accede mediante el protocolo POST, y la solicitud debe incluir una clave de API y el RFC que se desea consultar. Se proporciona una clave de API de prueba en este repositorio, que permite hasta 100 solicitudes diarias. Los usuarios son responsables de no exceder este límite. Si necesita una clave de API personal con más solicitudes, comuníquese con nosotros en [plusidentia@gmail.com](mailto:plusidentia@gmail.com) o abra un issue en este repositorio.

## Ejemplo usando curl
Un ejemplo para consultar la API usando curl es el siguiente:
```bash
curl -k -X 'POST' 'https://3.129.253.159/api/RFC/consulta_rfc' -H 'accept: text/plain' -H 'Content-Type: application/json' -d '{
  "apikey": "65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5",
  "rfc": "CVE2609105D1"
}'
```
## Ejemplo usando C#
```bash
using System;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;
using System.Net.Security;
using System.Security.Cryptography.X509Certificates;

class Program
{
    static async System.Threading.Tasks.Task Main()
    {
        string apiKey = "65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5";
        string rfcToQuery = "CVE2609105D1";

        // Ignore SSL certificate validation
        ServicePointManager.ServerCertificateValidationCallback = 
            new RemoteCertificateValidationCallback((sender, certificate, chain, sslPolicyErrors) => true);

        var httpClient = new HttpClient();
        var apiUrl = "https://3.129.253.159/api/RFC/consulta_rfc";

        var requestData = new
        {
            apikey = apiKey,
            rfc = rfcToQuery
        };

        var content = new StringContent(requestData.ToString(), Encoding.UTF8, "application/json");
        var response = await httpClient.PostAsync(apiUrl, content);

        if (response.IsSuccessStatusCode)
        {
            var result = await response.Content.ReadAsStringAsync();
            Console.WriteLine(result);
        }
        else
        {
            Console.WriteLine("Error: " + response.StatusCode);
        }
    }
}
```

## Ejemplo usando Python
```bash
import requests
import json
from requests.packages.urllib3.exceptions import InsecureRequestWarning

# Ignore SSL certificate validation
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)

api_url = "https://3.129.253.159/api/RFC/consulta_rfc"
api_key = "65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5"
rfc_to_query = "CVE2609105D1"

data = {
    "apikey": api_key,
    "rfc": rfc_to_query
}

headers = {
    "Content-Type": "application/json",
    "accept": "text/plain"
}

response = requests.post(api_url, data=json.dumps(data), headers=headers, verify=False)

if response.status_code == 200:
    result = response.text
    print(result)
else:
    print("Error:", response.status_code)
```
## Ejemplo usando java
```bash
import java.io.OutputStream;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import javax.net.ssl.HttpsURLConnection;
import javax.net.ssl.SSLContext;
import javax.net.ssl.TrustManager;
import javax.net.ssl.X509TrustManager;
import java.security.cert.X509Certificate;

public class RFCQuery {
    public static void main(String[] args) {
        String apiKey = "65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5";
        String rfcToQuery = "CVE2609105D1";

        // Ignore SSL certificate validation
        try {
            TrustManager[] trustAllCertificates = new TrustManager[]{
                new X509TrustManager() {
                    public X509Certificate[] getAcceptedIssuers() {
                        return null;
                    }
                    public void checkClientTrusted(X509Certificate[] certs, String authType) {
                    }
                    public void checkServerTrusted(X509Certificate[] certs, String authType) {
                    }
                }
            };

            SSLContext sslContext = SSLContext.getInstance("TLS");
            sslContext.init(null, trustAllCertificates, new java.security.SecureRandom());
            HttpsURLConnection.setDefaultSSLSocketFactory(sslContext.getSocketFactory());
        } catch (Exception e) {
            e.printStackTrace();
        }

        try {
            URL url = new URL("https://3.129.253.159/api/RFC/consulta_rfc");
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("POST");
            connection.setRequestProperty("Content-Type", "application/json");
            connection.setRequestProperty("accept", "text/plain");
            connection.setDoOutput(true);

            String jsonInputString = String.format("{\"apikey\": \"%s\", \"rfc\": \"%s\"}", apiKey, rfcToQuery);

            try (OutputStream os = connection.getOutputStream()) {
                byte[] input = jsonInputString.getBytes("UTF-8");
                os.write(input, 0, input.length);
            }

            try (BufferedReader br = new BufferedReader(
                    new InputStreamReader(connection.getInputStream(), "UTF-8"))) {
                StringBuilder response = new StringBuilder();
                String responseLine = null;
                while ((responseLine = br.readLine()) != null) {
                    response.append(responseLine.trim());
                }
                System.out.println(response.toString());
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Tenga en cuenta que debido a recursos limitados, la API tiene un certificado HTTPS autofirmado. Es posible que deba omitirlo en sus llamadas a la API para evitar errores.

## Tecnologías Utilizadas

Hemos implementado un Sistema de Automatización Robótica (RPA) que realiza consultas en tiempo real en el sitio web del SAT (Servicio de Administración Tributaria), resuelve captchas y realiza las consultas de RFC solicitadas. El sistema logra un rendimiento excelente y tiene una tasa de éxito del 100% en la resolución de captchas. Realizamos 10,000 pruebas y logró descifrar el captcha con éxito en todos los casos.

Para resolver captchas, utilizamos un modelo entrenado en TensorFlow.

## Estado del Proyecto

Este proyecto se mantiene activamente, y tenemos planes para realizar mejoras adicionales, que incluyen, pero no se limitan a:

    Reemplazar el certificado HTTPS autofirmado por uno válido.
    Implementar consultas masivas de RFC.

## Contacto

Para cualquier pregunta, aclaración, comentario o solicitud de una clave de API personal, no dude en comunicarse con nosotros en plusidentia@gmail.com o abrir un problema en este repositorio.
