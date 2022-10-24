# Image to Base64

### request
`POST`, JSON 형식으로 전송해야함

### Decode
```
byte[] data = Base64.getDecoder().decode(imgUrl);
ByteString imgBytes = ByteString.copyFrom(data);
```
