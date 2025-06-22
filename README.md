# Utilities Generator API

A MuleSoft RAML-based API for generating simulated utilities data for testing, development, and demonstration purposes.

## Overview

The Utilities Generator API provides realistic simulated data for utility companies and related systems without exposing real customer information. This API is designed to support development, testing, integration, and demo environments with consistent, controlled datasets covering meter readings, power consumption, outages, and fault events.

## Features

- **Meter Readings Generation**: Create realistic meter reading data for specified time periods
- **Power Consumption Analytics**: Generate hourly or daily consumption patterns
- **Outage Event Simulation**: Simulate power outage events with duration tracking
- **Fault Event Generation**: Create equipment failure and maintenance events
- **Configurable Time Ranges**: Generate data for any specified date range
- **Location-based Data**: Support for location-specific data generation
- **RESTful API Design**: Clean, intuitive endpoint structure
- **RAML 1.0 Specification**: Complete API documentation and contracts

## API Specification

### Base URL
```
/utilities/generate
```

### Data Types

#### MeterReading
```json
{
  "timestamp": "2024-03-20T10:00:00Z",
  "value": 1234.56
}
```

#### PowerConsumption
```json
{
  "timestamp": "2024-03-20T10:00:00Z",
  "consumption": 750.25
}
```

#### OutageData
```json
{
  "start_time": "2024-03-20T14:30:00Z",
  "end_time": "2024-03-20T16:45:00Z",
  "duration": "2h 15m"
}
```

#### FaultEvent
```json
{
  "timestamp": "2024-03-20T09:15:00Z",
  "type": "transformer_overload",
  "severity": "high"
}
```

## API Endpoints

### 1. Generate Meter Readings

Generate simulated meter readings for a specific meter and time period.

```http
GET /utilities/generate/meter-readings
```

**Required Parameters:**
- `start_date` (string): Start date (format: YYYY-MM-DD)
- `end_date` (string): End date (format: YYYY-MM-DD)
- `meter_id` (string): Unique meter identifier

**Example Request:**
```http
GET /utilities/generate/meter-readings?start_date=2024-01-01&end_date=2024-01-31&meter_id=MTR-001
```

**Example Response:**
```json
{
  "meter_id": "MTR-001",
  "readings": [
    {
      "timestamp": "2024-01-01T00:00:00Z",
      "value": 15234.67
    },
    {
      "timestamp": "2024-01-01T01:00:00Z",
      "value": 15237.23
    }
  ]
}
```

### 2. Generate Power Consumption

Generate simulated power consumption data with configurable intervals.

```http
GET /utilities/generate/power-consumption
```

**Required Parameters:**
- `start_date` (string): Start date (format: YYYY-MM-DD)
- `end_date` (string): End date (format: YYYY-MM-DD)
- `interval` (string): Data interval ("hourly" or "daily")

**Optional Parameters:**
- `location` (string): Location identifier

**Example Request:**
```http
GET /utilities/generate/power-consumption?start_date=2024-01-01&end_date=2024-01-07&interval=hourly&location=LOC-001
```

**Example Response:**
```json
{
  "location": "LOC-001",
  "consumption_data": [
    {
      "timestamp": "2024-01-01T00:00:00Z",
      "consumption": 850.45
    },
    {
      "timestamp": "2024-01-01T01:00:00Z",
      "consumption": 723.12
    }
  ]
}
```

### 3. Generate Outage Data

Generate simulated power outage events for analysis and testing.

```http
GET /utilities/generate/outage-data
```

**Required Parameters:**
- `start_date` (string): Start date (format: YYYY-MM-DD)
- `end_date` (string): End date (format: YYYY-MM-DD)

**Optional Parameters:**
- `location` (string): Location identifier

**Example Request:**
```http
GET /utilities/generate/outage-data?start_date=2024-01-01&end_date=2024-01-31&location=LOC-001
```

**Example Response:**
```json
{
  "location": "LOC-001",
  "outages": [
    {
      "start_time": "2024-01-15T14:30:00Z",
      "end_time": "2024-01-15T16:45:00Z",
      "duration": "2h 15m"
    },
    {
      "start_time": "2024-01-22T08:15:00Z",
      "end_time": "2024-01-22T08:45:00Z",
      "duration": "30m"
    }
  ]
}
```

### 4. Generate Fault Events

Generate simulated equipment fault and failure events.

```http
GET /utilities/generate/fault-events
```

**Required Parameters:**
- `start_date` (string): Start date (format: YYYY-MM-DD)
- `end_date` (string): End date (format: YYYY-MM-DD)

**Optional Parameters:**
- `location` (string): Location identifier

**Example Request:**
```http
GET /utilities/generate/fault-events?start_date=2024-01-01&end_date=2024-01-31&location=LOC-001
```

**Example Response:**
```json
{
  "location": "LOC-001",
  "fault_events": [
    {
      "timestamp": "2024-01-10T09:15:00Z",
      "type": "transformer_overload",
      "severity": "high"
    },
    {
      "timestamp": "2024-01-18T13:22:00Z",
      "type": "line_fault",
      "severity": "medium"
    }
  ]
}
```

## Use Cases

### Development and Testing
- **Unit Testing**: Generate consistent test data for utility management systems
- **Integration Testing**: Test system integrations with realistic data patterns
- **Load Testing**: Generate large volumes of data for performance testing
- **End-to-End Testing**: Support complete workflow testing without real customer data

### Demo and Training
- **Product Demonstrations**: Showcase utility management features with realistic data
- **Training Environments**: Provide safe, controlled data for user training
- **Proof of Concepts**: Support pilot projects and prototypes

### Data Analysis
- **Algorithm Testing**: Test analytics and machine learning algorithms
- **Reporting Validation**: Validate reporting systems with known data patterns
- **Dashboard Development**: Populate dashboards and visualizations during development

## Technical Specifications

### Technology Stack
- **API Specification**: RAML 1.0
- **Platform**: MuleSoft Anypoint Platform
- **Exchange Integration**: Deployable to MuleSoft Exchange
- **Response Format**: JSON

### Project Structure
```
/
├── utilities-generator-api.raml          # Main API specification
├── exchange.json                         # MuleSoft Exchange metadata
├── Utilities Generator API.code-workspace # VS Code workspace
├── .mvn/                                # Maven configuration
├── .exchange_modules_tmp/               # Build artifacts
└── .vscode/                             # VS Code settings
```

## Installation and Deployment

### Prerequisites
- MuleSoft Anypoint Studio or Design Center
- Access to MuleSoft Anypoint Platform
- Maven (for local builds)

### Local Development

1. **Clone the repository:**
```bash
git clone https://github.com/msaleme/Utilities-Generator-API.git
cd Utilities-Generator-API
```

2. **Open in Anypoint Studio:**
   - Import the project into Anypoint Studio
   - The RAML specification will be automatically recognized

3. **Design Center Alternative:**
   - Upload the `utilities-generator-api.raml` file to Design Center
   - Use the visual editor for modifications

### MuleSoft Exchange Deployment

1. **Publish to Exchange:**
```bash
mvn clean deploy
```

2. **Exchange Configuration:**
   - Group ID: `7e6f8241-36d8-45cf-abb7-2048a629ae51`
   - Asset ID: `utilities-generator-api`
   - Version: `1.0.0`

### Implementation Options

#### Option 1: MuleSoft Implementation
- Create a Mule application implementing the RAML specification
- Deploy to CloudHub or on-premises Mule runtime
- Use DataWeave for data generation logic

#### Option 2: API-Led Connectivity
- Use as a contract-first approach for API development
- Implement the backend with any technology stack
- Ensure compliance with the RAML specification

## API Documentation

### Interactive Documentation
The RAML specification provides interactive documentation that includes:
- Complete endpoint descriptions
- Request/response examples
- Data type definitions
- Parameter validation rules

### Viewing Documentation
1. **MuleSoft Exchange**: View published documentation
2. **API Console**: Use RAML console for interactive testing
3. **Anypoint Studio**: Built-in documentation viewer

## Data Generation Patterns

### Realistic Data Simulation
The API is designed to generate realistic utility data patterns:

- **Meter Readings**: Progressive incremental values
- **Power Consumption**: Daily and seasonal usage patterns
- **Outages**: Random but realistic outage durations
- **Fault Events**: Various equipment failure types and severities

### Configurable Parameters
- **Time Ranges**: Any date range for historical or future data
- **Intervals**: Hourly, daily, or custom intervals
- **Locations**: Multi-location support for complex scenarios
- **Volume**: Scalable data generation for different testing needs

## Error Handling

The API follows standard HTTP status codes:

- `200 OK`: Successful data generation
- `400 Bad Request`: Invalid parameters or date ranges
- `404 Not Found`: Invalid endpoint
- `500 Internal Server Error`: Data generation failure

Example error response:
```json
{
  "error": {
    "code": "INVALID_DATE_RANGE",
    "message": "End date must be after start date",
    "details": {
      "start_date": "2024-01-31",
      "end_date": "2024-01-01"
    }
  }
}
```

## Security Considerations

- **No Real Data**: All generated data is simulated and contains no real customer information
- **Rate Limiting**: Implement appropriate rate limiting for production use
- **Authentication**: Add authentication layers as needed for your environment
- **Data Retention**: Generated data should not be persisted beyond testing needs

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Update the RAML specification as needed
4. Test your changes in Anypoint Studio or Design Center
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

## RAML Best Practices

This API follows RAML 1.0 best practices:
- Clear data type definitions
- Consistent naming conventions
- Comprehensive documentation
- Proper parameter validation
- Example requests and responses

## License

This project is licensed under the terms specified in the project documentation.

## Support

For questions, issues, or contributions:
- Open an issue on GitHub
- Check MuleSoft community forums for RAML-specific questions
- Review MuleSoft documentation for platform-specific guidance

## Roadmap

Future enhancements may include:
- [ ] Additional utility data types (gas, water, solar)
- [ ] More sophisticated data generation algorithms
- [ ] WebSocket support for real-time data streaming
- [ ] GraphQL API specification
- [ ] Advanced filtering and aggregation options
- [ ] Custom data pattern templates

## Author

Mike Saleme - [GitHub](https://github.com/msaleme)

## Related Resources

- [RAML 1.0 Specification](https://raml.org/)
- [MuleSoft Exchange](https://www.mulesoft.com/exchange/)
- [Anypoint Platform](https://www.mulesoft.com/platform/enterprise-integration)
- [API-Led Connectivity](https://www.mulesoft.com/resources/api/api-led-connectivity)