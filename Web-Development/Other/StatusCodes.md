```ts
throw new BadRequestException('Bad request');
throw new UnauthorizedException('Unauthorized');
throw new ForbiddenException('Forbidden');
throw new NotFoundException('Not found');
throw new MethodNotAllowedException('Method not allowed');
throw new NotAcceptableException('Not acceptable');
throw new RequestTimeoutException('Request timeout');
throw new ConflictException('Conflict');
throw new GoneException('Gone');
throw new PayloadTooLargeException('Payload too large');
throw new UnsupportedMediaTypeException('Unsupported media type');
throw new UnprocessableEntityException('Unprocessable entity');
throw new InternalServerErrorException('Internal server error');
throw new NotImplementedException('Not implemented');
throw new BadGatewayException('Bad gateway');
throw new ServiceUnavailableException('Service unavailable');
throw new GatewayTimeoutException('Gateway timeout');
```


```ts
BadRequestException               → 400
UnauthorizedException             → 401
ForbiddenException                → 403
NotFoundException                 → 404
MethodNotAllowedException         → 405
NotAcceptableException            → 406
RequestTimeoutException           → 408
ConflictException                 → 409
GoneException                     → 410
PayloadTooLargeException          → 413
UnsupportedMediaTypeException     → 415
UnprocessableEntityException      → 422

InternalServerErrorException      → 500
NotImplementedException           → 501
BadGatewayException               → 502
ServiceUnavailableException       → 503
GatewayTimeoutException           → 504
```
