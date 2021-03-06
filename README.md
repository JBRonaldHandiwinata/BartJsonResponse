# BartJsonResponse
Custom starlette JSONResponse to avoid automatic lowercase header key conversion in FastAPI

### Implementation in FastAPI:
```bash
    from fastapi import APIRouter
    from bart_header import BartJSONResponse
    
    router = APIRouter()

    @router.post("/headers")
    def showme_headers():
        content = {"message": "Hello World"}
        sign = "hohohohohoho"
        header = {
            "Content-Type": "application/json; charset=UTF-8",
            "Client-Id": "blablabla",
            "Response-Time": "2020091067404843557525",
            "Signature": "algorithm=AES, signature=" + sign
        }

        return BartJSONResponse(content=content, headers=header)
```

### The response header received by client would be like:
```bash
{'date': 'Thu, 23 Sep 2021 15:58:58 GMT', 'server': 'uvicorn', 
'Content-Type': 'application/json; charset=UTF-8, application/json', 
'Client-Id': 'blablabla', 'Response-Time': '2020091067404843557525', 
'Signature': 'algorithm=AES, signature=hohohohohoho', 
'content-length': '25'}
```

### Limitation
1. For the time being only to handle json response