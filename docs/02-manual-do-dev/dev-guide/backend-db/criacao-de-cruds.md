
# Criação de CRUDs

##### Esta página contém as instruções para a criação dos endpoints básico para CRUDs em entitades dentro do sistema E-SUS urgências.

##### - Criação da estrutura básica

O nestJS fornece um CLI (command-line interface) que facilita o scaffolding de uma nova entidade no sistema. Neste documento, teremos as instruções básicas para criação da estrutura que precisaremos para implementação de endpoints de CRUD.  
  
Primeiramente, precisamos instalar o Nest CLI. Para isso, podemos executar o seguinte comando:

```bash
$ npm install -g @nestjs/cli
```

Após a instalação, podemos verificar se a instalação foi bem sucedida com o seguinte comando:

```bash
nest --version
```

Em caso de sucesso, a versão atual do NestCLI deve aparecer:  
  
[![image.png](/img/criacao-de-cruds-1.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-01/6wCm1xTfgv3aa784-image.png)

Após isso, dentro do repositório do projeto, navege, utilizando o terminal, até o diretório /backend. Uma vez dentro desse diretório, utilize os seguintes comando para criação do **Module**, **Service**, e **Controller**.

 Para mais informações sobre o NestCLI, podemos consultar a documentação oficial em: https://docs.nestjs.com/cli/overview

**OBS:** Nesse exemplo, queremos criar uma entidade "Time/Equipe", que aqui chamaremos de /team. Substitua esse nome pelo nome do módulo que deseja criar

```bash
nest generate module /team
```

```bash
nest generate service /team
```

```bash
nest generate controller /team
```

Ao inserir cada comando, será solicitado em qual projeto queremos criar esse novo módulo. Nesse caso, selecionaremos "api"

  
[![image.png](/img/criacao-de-cruds-2.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-01/kLZ9i2KeG3GMS9fO-image.png)

Feito isso, teremos a seguinte estrutura dentro de /backend/apps/api/src  
  
[![image.png](/img/criacao-de-cruds-3.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-01/JR054EHAjO3erLc2-image.png)

Note que uma pasta **/team** foi criada dentro de **/src**, bem como nosso service, controller e module.

Para finalizar, dentro de **/team** vamos criar o diretório **/dto** e **/entities**, para armazenar, respectivamente, os **DTOs** (Data transfer objects) e nossa definição de **Entidade**. Ademais, criaremos **manualmente**, dentre de seus respectivos diretórios, os arquivos **team.dto.ts** e **team.entity.ts**.

Por fim, teremos a seguinte estrutura dentro de **/team**:

**OBS:** Arquivos com a extensão **.spec** são arquivos de teste. Eles são gerados automaticamente pelo CLI do nestJS. Vamos apagá-los, por momento. Podemos recriá-los manualmente, futuramente, caso presisemos.

[![image.png](/img/criacao-de-cruds-4.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-01/7zEoIOcXeWJYnZbF-image.png)

##### - Definições da Entidade e DTOs

Primeiramente, devemos declarar quais atributos nossa entidade terá. Para isso, dentro de **team.entity.ts**, devemos ter:

```javascript
import { Entity, Column, PrimaryGeneratedColumn } from 'typeorm';

@Entity()
export class Team {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;
}
```

Atente-se que o NestJS é "database agnostic", ou seja, ele não possui um ORM padrão. No projeto do E-SUS Urgências, estamos utilizando o **TypeORM**. Podemos dizer que essa classe é uma entidade usando o decorator **@Entity()**. Aqui estamos apenas declarando 2 campos básicos, **id** e **name**. Cada atributo é precedido por um decorator para definir o comportamento daquele atributo. Para mais informações sobre os decorators, visite: https://typeorm.io/entities  
  
Ademais, vamos criar o seguinte DTO dentro de **team.dto.ts:**

```javascript
export class CreateTeamDto {
  name: string;
}
```

##### - Definições dos services e controllers

Agora, podemos começar a definir os nossos services, para tal, dentro de **team.service.ts**, podemos adicionar o seguinte:

```javascript
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { Team } from './entities/team.entity';
import { CreateTeamDTO } from './dto/team.dto';

@Injectable()
export class TeamService {
  constructor(
    @InjectRepository(Team)
    private teamRepository: Repository<Team>,
  ) {}

  // Create
  async create(createTeamDto: CreateTeamDTO): Promise<Team> {
    const team = this.teamRepository.create(createTeamDto);
    return this.teamRepository.save(team);
  }

  // Retrieve
  async findAll(): Promise<Team[]> {
    return this.teamRepository.find();
  }

  // Update
  async update(id: number, updateTeamDto: CreateTeamDTO): Promise<Team> {
    const team = await this.teamRepository.findOne({ where: { id } });
    if (!team) {
      throw new Error('Equipe não encontrada');
    }
    this.teamRepository.merge(team, updateTeamDto);
    return this.teamRepository.save(team);
  }

  // Delete
  async delete(id: number): Promise<Team> {
    const team = await this.teamRepository.findOne({ where: { id } });
    if (!team) {
      throw new Error('Equipe não encontrada');
    }
    return this.teamRepository.remove(team);
  }
}
```

**OBS:** Note que essa são operações simples de CRUD. Alterações no fluxo e tratamentos de erro devem ser feitos conforme as regras de negócio.

Da mesma forma, podemos definir nossos endpoints em **team.controller.ts**:

```javascript
import { Controller, Post, Body, Get, Put, Delete, Param } from '@nestjs/common';
import { TeamService } from './team.service';
import { CreateTeamDTO } from './dto/team.dto';
import { Team } from './entities/team.entity';

@Controller('team')
export class TeamController {
  constructor(private readonly teamService: TeamService) {}

  @Post()
  async create(@Body() createTeamDto: CreateTeamDTO): Promise<Team> {
    return this.teamService.create(createTeamDto);
  }

  @Get()
  async findAll(): Promise<Team[]> {
    return this.teamService.findAll();
  }

  @Put(':id')
  async update(
    @Param('id') id: number,
    @Body() updateTeamDto: CreateTeamDTO
  ): Promise<Team> {
    return this.teamService.update(id, updateTeamDto);
  }

  @Delete(':id')
  async delete(@Param('id') id: number): Promise<Team> {
    return this.teamService.delete(id);
  }
}
```

Assim, teremos as seguintes rotas:  
  
**POST** http://&lt;api-url&gt;/team

**GET** http://&lt;api-url&gt;/team

**PUT** http://&lt;api-url&gt;/team/:id

**DELETE** http://&lt;api-url&gt;/team/:id

##### - Injeções de dependência e módulos

Por fim, devemos integrar nosso novo módulo "team" com nosso módulo de aplicação principal, além de injetar as dependências que nosso service solicita (no nosso caso, o repositório). Para tal, dentro de **team.module.ts** vamos adicionar o seguinte:

```javascript
import { Module } from '@nestjs/common';
import { TeamService } from './team.service';
import { TeamController } from './team.controller';
import { TypeOrmModule } from '@nestjs/typeorm';
import { Team } from './entities/team.entity';

@Module({
  imports: [TypeOrmModule.forFeature([Team])],
  providers: [TeamService],
  controllers: [TeamController]
})
export class TeamModule {}
```

Por fim, dentro de **/src/app.module.ts** devemos adicionar nossa entidade dentro da lista "entities". Ademais, devemos conferir se nosso módulo "TeamModule" foi importando dentro do módulo principal (O nestCLI deve fazer isso automaticamente, mas é sempre legal conferir).

Teremos:

```javascript
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { ItemsModule } from './items/items.module';
import { KafkaService } from './kafka/kafka.service';
import { Item } from './items/entities/item.entity';
import { Ambulance } from './ambulance/entities/ambulance.entity';
import { Profile } from './profile/entities/profile.entity';
import { CallSource } from './call_source/entities/call_source.entity';
import { CallType } from './call_type/entities/call_type.entity';
import { JobTitle } from './job_title/entities/job_title.entity';
import { Team } from './team/entities/team.entity';
import { Occurrence } from './occurrence/entities/occurence.entity';
import { AmbulanceModule } from './ambulance/ambulance.module';
import { ProfileModule } from './profile/profile.module';
import { CallSourceModule } from './call_source/call_source.module';
import { CallTypeModule } from './call_type/call_type.module';
import { JobTitleModule } from './job_title/job_title.module';
import { OccurrenceModule } from './occurrence/occurrence.module';
import { TeamModule } from './team/team.module';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: <type>,
      host: process.env.DB_HOST || <host>,
      port: parseInt(process.env.DB_PORT) || ,
      username: process.env.DB_USER || <username>,
      password: process.env.DB_PASSWORD || ,
      database: process.env.DB_NAME || <databaseName>,
      entities: [Item, Ambulance, Profile, CallSource, CallType, JobTitle, Occurrence, Team],
      synchronize: true,
      autoLoadEntities: true,
    }),
    ItemsModule,
    AmbulanceModule,
    ProfileModule,
    CallSourceModule,
    CallTypeModule,
    JobTitleModule,
    OccurrenceModule,
    TeamModule,
  ],
  providers: [KafkaService],
})
export class AppModule {}
```

**OBS**: Note que algumas informações foram ocultadas e substituidas por **&lt;something&gt;**, não estando sintaticamente corretas.

Finalmente, podemos buildar nosso projeto e testar nossos endpoints:

**POST:**

[![image.png](/img/criacao-de-cruds-5.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-01/ISKTSZ0DVC6gRvw9-image.png)  
  
**GET:**

[![image.png](/img/criacao-de-cruds-6.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-01/yIEszPDBI9NtbFEW-image.png)

##### - Swagger e ducumentação

O módulo no swagger do nestJS está configurado para adicionar automaticamente qualquer endpoint criado à documentação swagger. Para acessar a documentação, acesse a url http://&lt;api-url&gt;/api (link padrão) ou o link que estiver indicado pela variável SWAGGER\_URL