# RFC-Consulta-API

[Leer este README en Español](README.md)

## Description
This repository provides a user-friendly REST API for querying RFC (Registro Federal de Contribuyentes) information in Mexico.

## Usage Instructions
At the moment, the API is accessible from any device with internet access. The API is accessed via the POST protocol, and the request should include an API key and the RFC to be queried. A test API key is provided in this repository, which allows up to 100 daily requests. Users are responsible for not exceeding this limit. If you need a personal API key with more requests, please contact us at [plusidentia@gmail.com](mailto:plusidentia@gmail.com) or open an issue in this repository.

An example for querying the API using curl is as follows:
```bash
curl -k -X 'POST' 'https://3.129.253.159/api/RFC/consulta_rfc' -H 'accept: text/plain' -H 'Content-Type: application/json' -d '{
  "apikey": "65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5",
  "rfc": "CVE2609105D1"
}'
```

Please note that due to limited resources, the API has a self-signed HTTPS certificate. You may need to ignore it in your API calls to avoid errors.

## Technologies Used
We have implemented a Real Person API (RPA) that performs real-time queries on the SAT (Servicio de Administración Tributaria) website, solves captchas, and conducts the requested RFC queries. The system achieves excellent performance and has a 100% success rate in captcha solving. We conducted 10,000 tests, and it successfully deciphered the captcha in all cases.

For captcha solving, we utilize a trained model in TensorFlow.

## Project Status
This project is actively maintained, and we have plans for further improvements, including but not limited to:

1. Replacing the self-signed HTTPS certificate with a valid one.
2. Implementing bulk RFC queries.

## Contact
For any questions, clarifications, comments, or requests for a personal API key, please feel free to reach out to us at [plusidentia@gmail.com](mailto:plusidentia@gmail.com) or open an issue in this repository.
