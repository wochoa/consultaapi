# API Consulta Ruc y Dni - Perú

[![Github Actions](https://github.com/giansalex/peru-consult-api/workflows/CI/badge.svg)](https://github.com/giansalex/peru-consult-api/actions)
[![docker](https://github.com/giansalex/peru-consult-api/actions/workflows/docker-publish.yml/badge.svg)](https://github.com/giansalex/peru-consult-api/actions/workflows/docker-publish.yml)
[![Docker Pulls](https://img.shields.io/docker/pulls/giansalex/peru-consult-api.svg?style=flat-square)](https://hub.docker.com/r/giansalex/peru-consult-api)
[![GitHub issues](https://img.shields.io/github/issues/giansalex/peru-consult-api.svg?style=flat-square)](https://github.com/giansalex/peru-consult-api/issues)  
API para consultar el DNI y RUC - Perú, empleando [peru-consult](https://github.com/giansalex/peru-consult) package.


## Requerimientos

- PHP 7.4 o superior.

## Instalar

### Docker

Usar la imagen desde [Docker Hub](https://hub.docker.com/r/giansalex/peru-consult-api/)
```bash
docker run -d -p 8080:8080 --name peru-consult -e API_TOKEN=your_key giansalex/peru-consult-api
```

### Construir desde codigo fuente

```
git clone https://github.com/giansalex/peru-consult-api.git
cd peru-consult-api
composer install
php -S 0.0.0.0:8080 -t public
```

## Ejemplos

### GraphQL
Implementando soporte para [graphql](http://graphql.org/) utilizar el endpoint `/api/graph`   

```
query {
    person(dni: "48004836") {
    	dni
    	nombres
    },
    company(ruc: "20131312955") {
    	ruc
    	razonSocial
    }
}
```
Respuesta:
```json
{
    "data": {
        "person": {
            "dni": "48004836",
            "nombres": "ROBERTO CARLOS"
        },
        "company": {
            "ruc": "20131312955",
            "razonSocial": "SUPERINTENDENCIA NACIONAL DE ADUANAS Y DE ADMINISTRACION TRIBUTARIA - SUNAT"
        }
    }
}
```

### DNI
Ejecutar usando Curl.
```bash
curl -H "Accept: application/json" http://localhost:8080/api/v1/dni/48004836?token=abcxyz
```

Respuesta:

```json
{
  "dni": "48004836",
  "nombres": "ROBERTO CARLOS",
  "apellidoPaterno": "SULCA",
  "apellidoMaterno": "BASILIO",
  "codVerifica": "4"
}
```

### RUC
Ejecutar usando Curl.
```bash
curl -H "Accept: application/json" http://localhost:8080/api/v1/ruc/20131312955?token=abcxyz
```

Respuesta:

```json
{
  "ruc": "20131312955",
  "razonSocial": "SUPERINTENDENCIA NACIONAL DE ADUANAS Y DE ADMINISTRACION TRIBUTARIA - SUNAT",
  "nombreComercial": "-",
  "tipo": "INSTITUCIONES PUBLICAS",
  "estado": "ACTIVO",
  "condicion": "HABIDO",
  "direccion": "AV. GARCILASO DE LA VEGA NRO. 1472",
  "departamento":"LIMA",
  "provincia":"LIMA",
  "distrito":"LIMA",
  "fechaInscripcion": "1993-05-04T00:00:00.000Z",
  "sistEmsion": "MANUAL/COMPUTARIZADO",
  "sistContabilidad": "COMPUTARIZADO",
  "actExterior": "SIN ACTIVIDAD",
  "actEconomicas": [
    "75113 - ACTIV. ADMINIST. PUBLICA EN GENERAL"
  ],
  "cpPago": [
    "FACTURA",
    "BOLETA DE VENTA",
    "NOTA DE CREDITO",
    "NOTA DE DEBITO",
    "GUIA DE REMISION - REMITENTE",
    "COMPROBANTE DE RETENCION",
    "POLIZA DE ADJUDICACION POR REMATE DE BIENES"
  ],
  "sistElectronica": [
    "FACTURA PORTAL                      DESDE 07/08/2013",
    "BOLETA PORTAL                       DESDE 01/04/2016"
  ],
  "fechaEmisorFe": "2013-08-07T00:00:00.000Z",
  "cpeElectronico": [
    "FACTURA (desde 07/08/2013)",
    "BOLETA (desde 01/04/2016)"
  ],
  "fechaPle": "2013-01-01T00:00:00.000Z",
  "padrones": [
    "Incorporado al Régimen de Agentes de Retención de IGV (R.S.037-2002) a partir del 01/06/2002"
  ],
  "fechaBaja": null,
  "profesion": ""
}
```

### Consulta Validez Usuario SOL
Ejecutar usando Curl.
```bash
curl http://localhost:8080/api/v1/user-sol/20000000001/GMABCI?token=abcxyz
```

Respuesta:

```text
true
```


### GraphiQL Tool
Para mejorar aún más nuestra experiencia en pruebas, sugerimos comenzar a utilizar el cliente GraphiQL.
Es un Explorador de esquema GraphQL que puede descargar desde Chrome Store. Utilizar el endpoint `/api/v1/graph`, el editor tiene una función de autocompletar y contiene toda la información sobre el esquema actual en el lado derecho en la barra lateral de Documentos:
![GraphiQL Interface](https://raw.githubusercontent.com/giansalex/peru-consult-api/master/docs/screenshot-graph.png)
