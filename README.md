# RFC-Consulta-API

[Read this README in English](README_eng.md)

## Descripción
Este repositorio proporciona una API REST fácil de usar para consultar información del RFC (Registro Federal de Contribuyentes) en México.

## Instrucciones de Uso
Por el momento, la API es accesible desde cualquier dispositivo con acceso a Internet. La API se accede mediante el protocolo POST, y la solicitud debe incluir una clave de API y el RFC que se desea consultar. Se proporciona una clave de API de prueba en este repositorio, que permite hasta 100 solicitudes diarias. Los usuarios son responsables de no exceder este límite. Si necesita una clave de API personal con más solicitudes, comuníquese con nosotros en [plusidentia@gmail.com](mailto:plusidentia@gmail.com) o abra un problema en este repositorio.

Un ejemplo para consultar la API usando curl es el siguiente:
```bash
curl -k -X 'POST' 'https://3.129.253.159/api/RFC/consulta_rfc' -H 'accept: text/plain' -H 'Content-Type: application/json' -d '{
  "apikey": "65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5",
  "rfc": "CVE2609105D1"
}'
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
