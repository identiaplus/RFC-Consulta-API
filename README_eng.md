# RFC-Consulta-API

[Leer este README en Español](README.md)

## Description
This repository provides a user-friendly REST API for querying RFC (Registro Federal de Contribuyentes) information in Mexico.

## Usage Instructions
At the moment, the API is accessible from any device with internet access. The API is accessed via the POST protocol, and the request should include an API key and the RFC to be queried. A test API key is provided in this repository, which allows up to 100 daily requests. Users are responsible for not exceeding this limit. If you need a personal API key with more requests, please contact us at [plusidentia@gmail.com](mailto:plusidentia@gmail.com) or open an issue in this repository.

## Example using curl
An example to query the API using curl is the following:
```bash
curl -k -X 'POST' 'https://3.129.253.159/api/RFC/consulta_rfc' -H 'accept: text/plain' -H 'Content-Type: application/json' -d '{
  "apikey": "65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5",
  "rfc": "CVE2609105D1"
}'
```
## Example using C#
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

## Example using Python
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
## Example using java
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

Please note that due to limited resources, the API has a self-signed HTTPS certificate. You may need to omit it in your API calls to avoid errors.

## Technologies Used
We have implemented a Real Person API (RPA) that performs real-time queries on the SAT (Servicio de Administración Tributaria) website, solves captchas, and conducts the requested RFC queries. The system achieves excellent performance and has a 100% success rate in captcha solving. We conducted 10,000 tests, and it successfully deciphered the captcha in all cases.

For captcha solving, we utilize a trained model in TensorFlow.

## Project Status
This project is actively maintained, and we have plans for further improvements, including but not limited to:

1. Replacing the self-signed HTTPS certificate with a valid one.
2. Implementing bulk RFC queries.

## Contact
For any questions, clarifications, comments, or requests for a personal API key, please feel free to reach out to us at [plusidentia@gmail.com](mailto:plusidentia@gmail.com) or open an issue in this repository.
