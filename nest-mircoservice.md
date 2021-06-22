# Nest CLI Documentation :
```
$ npm install -g @nestjs/cli
$ nest new my-nest-pro
$ cd my-nest-pro
$ npm run start:dev
$ nest g cl data  //Generate class and spec file
$ nest g co test  // Generate controller, spec and register app.module file 
$ nest g mo product // Generate Module and register app.module file
$ nest g s productService // Generate service, spec and register app.module file 
$ nest g in interceptorHttp // create Interceptors 

```
# API Swagger Documentation :
### 3 Steps follow as below :
```
[1] npm install --save @nestjs/swagger swagger-ui-express

[2] import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

[3]  const config = new DocumentBuilder()
    .setTitle('Rajendra Microservice Example')
    .setDescription('Standard microservice with all features')
    .setVersion('1.0')
    .addTag('rt')
    .build();

  const app = await NestFactory.create(AppModule);
  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api', app, document);
```
# Nest Microservice ServerSide code snippet :

### Sample math.service.ts :
```
import { Injectable } from '@nestjs/common';

@Injectable()
export class MathService {
    public accumulate(data: number[]): number {
        return (data || []).reduce((a, b) => Number(a) + Number(b));
    }
}
```
### Sample app.controller.ts :
```
import { Controller, Logger, Post, Body } from '@nestjs/common';
import { MathService } from './math.service';
import { MessagePattern } from '@nestjs/microservices';

@Controller()
export class AppController {
  // Create a logger instance
  private logger = new Logger('AppController');

  // Inject the math service
  constructor(private mathService: MathService) {}

  // Define the message pattern for this method
  @MessagePattern('add')
  // Define the logic to be executed
  async accumulate(data: number[])  {
    this.logger.log('Adding ' + data.toString()); // Log something on every call
    return this.mathService.accumulate(data); // use math service to calc result & return
  }
}
```
### Sample app.module.ts :
```
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { MathService } from './math.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [MathService],
})
export class AppModule {}
```
### Sample main.ts :
```
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { MathService } from './math.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [MathService],
})
export class AppModule {}
```
# Nest Microservice Client code snippet :
### Sample math.service.ts :
```
import { Injectable } from '@nestjs/common';
import { ClientProxyFactory, Transport, ClientProxy } from '@nestjs/microservices';

@Injectable()
export class MathService {
  private client: ClientProxy;

  constructor() {
    this.client = ClientProxyFactory.create({
      transport: Transport.TCP,
      options: {
        host: '127.0.0.1',
        port: 8877,
      },
    });
  }

  public accumulate(data: number[]) {
    return this.client.send<number, number[]>('add', data);
  }
}
```
### Sample app.controller.ts :
```
import { Controller, Logger, Post, Body } from '@nestjs/common';
import { MathService } from './math.service';

@Controller()
export class AppController {
  // Create a logger instance
  private logger = new Logger('AppController');

  // Inject the math service
  constructor(private mathService: MathService) {}

  // Map the 'POST /add' route to this method
  @Post('add')
  // Define the logic to be executed
  async accumulate(@Body('data') data: number[])  {
    this.logger.log('Adding ' + data.toString()); // Log something on every call
    return this.mathService.accumulate(data); // use math service to calc result & return
  }
}
```
### Sample app.module.ts :
```
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { MathService } from './math.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [MathService],
})
export class AppModule {}
```
### Sample main.ts :
```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();

```


