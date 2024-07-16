# NCPeH API Integration

## Overview

The National Contact Point for eHealth (NCPeH) API facilitates the secure exchange of health information across borders within the European Union. This API ensures that patient data can be accessed and shared seamlessly between different healthcare systems, enhancing the continuity of care for patients traveling or living abroad.

## Implementation Details

### API Endpoints

The NCPeH API provides several endpoints for different functionalities, including patient summaries, ePrescriptions, and more. Below are the primary endpoints:

- **Patient Summary Endpoint**: `/api/patient-summary`
- **ePrescription Endpoint**: `/api/eprescription`
- **Document Retrieval Endpoint**: `/api/document-retrieval`

### Authentication

The NCPeH API uses OAuth 2.0 for authentication. Ensure that your application is registered with the NCPeH system to obtain the necessary client ID and secret.

#### Example Authentication Request

```http
POST /oauth/token
Host: ncpeh.example.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET
```

### Data Formats

The API supports data exchange in HL7 FHIR and HL7 CDA formats. Ensure that your system can handle these formats for both sending and receiving data.

### Error Handling

The API returns standard HTTP status codes to indicate the success or failure of a request. Implement appropriate error handling in your system to manage these responses.

- **200 OK**: The request was successful.
- **400 Bad Request**: The request was invalid or cannot be served.
- **401 Unauthorized**: Authentication failed or user does not have permissions.
- **500 Internal Server Error**: An error occurred on the server.

## Usage Examples

### Retrieving a Patient Summary

```http
GET /api/patient-summary?patient_id=12345
Host: ncpeh.example.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Accept: application/fhir+json
```

### Submitting an ePrescription

```http
POST /api/eprescription
Host: ncpeh.example.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/fhir+json

{
  "resourceType": "MedicationRequest",
  "id": "example",
  "status": "active",
  "intent": "order",
  "medicationCodeableConcept": {
    "coding": [
      {
        "system": "http://www.nlm.nih.gov/research/umls/rxnorm",
        "code": "860975",
        "display": "Amoxicillin 250mg/5ml Suspension"
      }
    ]
  },
  "subject": {
    "reference": "Patient/12345"
  },
  "authoredOn": "2023-10-01",
  "requester": {
    "reference": "Practitioner/1"
  }
}
```

## References

- [NCPeH Official Documentation](https://ec.europa.eu/health/ehealth/national-contact-points_en)
- [HL7 FHIR Specification](https://www.hl7.org/fhir/)
- [HL7 CDA Specification](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=7)

By following these guidelines and examples, you can ensure that your integration with the NCPeH API is robust and compliant with European standards for health information exchange.

