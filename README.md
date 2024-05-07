# quarkus-financial

This project provides a simple API to store and retrieve stock price data. It allows users to store stock prices by symbol and retrieve a list of stored stock data.

## System Requirements

The application requires JDK 21 to run.

## Compiling, Packaging, and Running the Application

To compile, package, and start the application in development mode for live coding, use:
```shell script
./mvnw compile quarkus:dev
```

## Testing

Run tests with:
```shell script
./mvnw test
```

## Endpoints

After the application is running, endpoints can be tested via Swagger UI at `localhost:8080/q/swaggerui`.

- `/stock/create` (POST): This endpoint requires a JSON body with the following structure:
```json
{
  "symbol": "AAPL"
}
```
If the symbol is found, data is stored in an H2 database and a response with the following structure is returned:
```json
{
  "id": 3,
  "symbol": "AAPL",
  "closePrice": 182.6665,
  "absoluteChange": 0.9565,
  "percentageChange": 0.5264,
  "highPrice": 184.9,
  "lowPrice": 182.31,
  "openPrice": 183.4,
  "previousClosePrice": 181.71,
  "timestamp": 1715094870
}
```
If the symbol is not found, no data is stored and the following response is returned:
```json
{
  "error_message": "The symbol 'PEPE' appears to not exist"
}
```

- `/stock/list` (GET): This endpoint retrieves a list of stocks stored by the `/stock/create` endpoint. The response structure is as follows:
```json
[
  {
    "id": 1,
    "symbol": "AAPL",
    "closePrice": 182.75,
    "absoluteChange": 1.04,
    "percentageChange": 0.5723,
    "highPrice": 184.9,
    "lowPrice": 182.31,
    "openPrice": 183.4,
    "previousClosePrice": 181.71,
    "timestamp": 1715094827
  },
  {
    "id": 2,
    "symbol": "AAPL",
    "closePrice": 182.6665,
    "absoluteChange": 0.9565,
    "percentageChange": 0.5264,
    "highPrice": 184.9,
    "lowPrice": 182.31,
    "openPrice": 183.4,
    "previousClosePrice": 181.71,
    "timestamp": 1715094870
  },
  {
    "id": 3,
    "symbol": "AAPL",
    "closePrice": 182.6665,
    "absoluteChange": 0.9565,
    "percentageChange": 0.5264,
    "highPrice": 184.9,
    "lowPrice": 182.31,
    "openPrice": 183.4,
    "previousClosePrice": 181.71,
    "timestamp": 1715094870
  }
]
```

