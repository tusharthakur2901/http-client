# http-client
Lightweight HTTP client library for making API requests in JavaScript

### `http_client.py`
Implement the HTTP client in a separate Python file.
```python
import requests

class HttpClient:
    def __init__(self, base_url):
        self.base_url = base_url

    def get(self, endpoint, params=None, headers=None):
        url = self.base_url + endpoint
        response = requests.get(url, params=params, headers=headers)
        response.raise_for_status()
        return response

    def post(self, endpoint, data=None, json=None, headers=None):
        url = self.base_url + endpoint
        response = requests.post(url, data=data, json=json, headers=headers)
        response.raise_for_status()
        return response

    def put(self, endpoint, data=None, json=None, headers=None):
        url = self.base_url + endpoint
        response = requests.put(url, data=data, json=json, headers=headers)
        response.raise_for_status()
        return response

    def delete(self, endpoint, headers=None):
        url = self.base_url + endpoint
        response = requests.delete(url, headers=headers)
        response.raise_for_status()
        return response

# Example usage
if __name__ == "__main__":
    client = HttpClient(base_url="https://jsonplaceholder.typicode.com")

    # GET request
    response = client.get("/posts")
    print(response.json())

    # POST request
    data = {
        "title": "foo",
        "body": "bar",
        "userId": 1
    }
    response = client.post("/posts", json=data)
    print(response.json())

    # PUT request
    data = {
        "id": 1,
        "title": "foo",
        "body": "bar",
        "userId": 1
    }
    response = client.put("/posts/1", json=data)
    print(response.json())

    # DELETE request
    response = client.delete("/posts/1")
    print(response.status_code)
