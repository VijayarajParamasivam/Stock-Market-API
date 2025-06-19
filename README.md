# Stock-Market-API

## Overview
A comprehensive API wrapper for real-time stock market data with predictive analytics on future stock prices using Yfinance API. 

## Features
- Real-time stock data
- Historical stock data (daily, weekly, monthly, yearly)
- Stock price prediction
- User authentication and rate limiting

## Installation

1. **Clone the Repository:**

    ```sh
    git clone https://github.com/VijayarajParamasivam/Stock-Market-API.git
    ```
    
    ```sh
    cd Stock-Market-API
    ```

2. **Create and Activate Virtual Environment:**
    If Python 3.11 is your primary version,
   
    ```sh
    python -m venv venv
    ```
    
    Else install Python 3.11 and use its path to create virtual environment,

    ```sh
    [Python.exe Path] -m venv venv
    ```
    
    Activate virtual environment using
   
    ```sh
    venv\Scripts\activate
    ```

4. **Install Dependencies:**

    ```sh
    pip install -r requirements.txt
    ```

## Running the API

1. **Start the API Server:**

    ```sh
    uvicorn app.main:app --reload --port 8001
    ```

2. **Access Documentation:**
   - Swagger UI: `http://127.0.0.1:8001/docs`

## Authentication

- **Register:** `POST /user/register`
  
    ```sh
    curl -X POST "http://127.0.0.1:8001/register" -H "Content-Type: application/json" -d "{\"username\": \"[your-username]\", \"email\": \"[your-email]\", \"password\": \"[password]\"}"
    ```
  
- **Login + API key:** `POST /user/login`
  
    ```sh
    curl -X POST "http://127.0.0.1:8001/token" -H "Content-Type:application/x-www-form-urlencoded" -d "username=[your-username]&password=[your-password]"
    ```
    Returns an unique API key for your user id , copy it for further use...
    
- **Delete:** `DELETE /user/delete`
  
  ```sh
      curl -X DELETE "http://127.0.0.1:8001/user/delete" -H "Authorization: Bearer [your-api-key]"
  ```

## Endpoints

### `GET /stocks/{symbol}/current`
- **Description:** Retrieve current stock data for given company symbol.(Needs API key)
  
 ```sh
    curl -X GET "http://127.0.0.1:8001/stocks/[symbol]/current" -H "Authorization: Bearer [your-api-key]"
  ```
  
### `GET /stocks/{symbol}/historical`
- **Description:** Retrieve historical stock data.(Needs API key)
- **Parameters:**
  - `symbol`: Stock ticker symbol (e.g., AAPL)
  - `start_date`: Optional start date (YYYY-MM-DD)
  - `end_date`: Optional end date (YYYY-MM-DD)
  - `frequency`: Data frequency (daily, weekly, monthly, yearly)
  - `format`: Response format (json, csv, xml)
    
      ```sh
        curl -X GET "http://127.0.0.1:8001/stocks/[symbol]/historical?start_date=[start_date]&end_date=[end-date]&frequency=[frequency]&format=[format]" -H "Authorization: Bearer [your-api-key]"
      ```

### `GET /predict/{symbol}`
- **Description:** Predict future stock prices for respective company symbol.(Needs API key)
- **Parameters:**
  - `symbol`: Stock ticker symbol
  - `periods`: Number of days to predict (eg: 10)
    
      ```sh
          curl -X GET "http://127.0.0.1:8001/predict/[symbol]?periods=[periods]" -H "Authorization: Bearer [your-api-key]"
      ```

## Rate Limiting

- Rate limit is set to 10 requests per day per user for predictions.
- Rate limit is set to 50 requests per day per user for current price and history data.

## Error Handling

- **401 Unauthorized:** Invalid or missing API key.
- **400 Bad Request:** Invalid input parameters.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For any questions, please contact [vijayarj.p@gmail.com](mailto:vijayarj.p@gmail.com).
