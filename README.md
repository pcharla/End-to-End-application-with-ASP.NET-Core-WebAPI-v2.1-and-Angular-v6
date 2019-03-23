# End-to-End-application-with-ASP.NET-Core-WebAPI-v2.1-and-Angular-v6
#Global readme for my revision later
----------------------------------------------------------------------------------------------------------------------------------------
Section 1:
ASP.NET Core Web API, Entity Framework Core, Angular
Web API backend, angular front end
service/repository pattern on the backend, angular is a client side framework

Some features: Dating app
Register/login/Authenticate using JSON web tokens
Profile, photo gallery, drag and drop photo uploader, (store pics securely on the cloud)
view profile, view other's photo gallery, send personal messages and likes

Version information:
Asp.net core 2.1, Angular 6, Entity framework 2.1
HTML5 , CSS3, Node.js, Git, Bootstrap, SQLite, MS SQL Server
focused on object oriented programming

Download:
Angular/CLI, (Typescript best editor)VS CODE (also excellent support for c#)
postman- api development environment- query our api without needing to write any cleint side code, used extensively when testing web api
db browser for sqlite for development, SQL Server Management Studio
node js - javascript runtime - for developing angular application(server side javascript engine)
y: comes with npm- package ecosystem for getting js packages, packwges download and dependencies managing
(angular also comes with a development server which uses node js in the background, we can also make use of angular cli, packages we need)
asp.net core sdk (includes runtime)
rider from jetbrains with resharper extension (if visual studio does not work for you)

Walking skeleton: tiny implementation of system that performs small end to end fucntion
need not use final architecture, but shud link together the main architectural components, then architecture and functionality
evolve in parallel.

architectural components/parts:
Db, Object relational mapper, API, aNGUlar for ui, UI html css etc---> components of our app

DB-->ORM-->               API-->               SPA-->                HTML view(Client)
     entity framework                  fetch values via the api
	 allows api to send                from our spa angular app
	 queries 2 database     
	 
Steps:
create the web api project
review files that are created by dotnet cli(tool used to create web api)
ensure web api runs successfully
create a db using code first/model first approcah
source control
create the angular application
configure angular application to fetch data from our api (make http requests from angular)
bind data we get back from api to the html so we can display it on the page
add bootstrap and font awesome for basic presentation

Key points:

values pulled in via api from database
spa can talk to api which can talk to database and return the data and display it on the page
dotnet projetc is for web api
in dotnet sdk tool, dotnet cli (command prompt where you can type dotnet commands)
----------------------------------------------------------------------------------------------------------------------------------------
Section 3:
Entity Framework is the object relational mapper we are using, it is responsible for scaffolding models and creating database tables.
We use it to query our database (Entity Framework needs to know about our models also known as entities)

New Folder Data-->New class--> DataContext.cs (derived class of dbcontext) --> inherits from DbContext(using entityframeowk core)
it represents a session with database- used to query and save instances of our entities

db context must have an instance of dbcontext options, we pass these options open to the base constructor of dbcontext

public DataContext(DbContextOptions<DataContext> options) : base (options){}
In datacontext class, to tell entity Framework about our entitities, we give some properties of type DbSet like below
public Dbset<Value> (type/Class) Values (table name in sql once our database is created), Now we need to tell our application about this

startup.cs: in configure services, we add that as a service: anything that is added as a service is available to be injected into any part of the application like below
services.AddDbcontext<DataContext>(x =>x.UseSqlite(Configuration.GetConnectionString("DefaultConnection")))
                                  some options
								  
use nuget package manager to install sqlite, can add connection strings to app settings.json

migrations incrementally apply changes to dataabse to keep it in sync with entity framwork core model while preserving data in the database

when we add a migration entity framework is taking a look at data context class and creates tables based on dbsets
add initial migration with whatever tables you  need

datacontext model snapshot is entity framework's way of tracking which migrations have been applied, so it doesnt need to query the 
database to know the same, designer.cs file-->used to decide what to remove from data conetxt model snapshot so entity framework understands where we are in terms of migrations, Entity framework is convention based

if we wanna rollback a  migration, after we have applied then down method in migration executes

creating data and seeding data into our database? what is it, what are the better ways to do it
Now to extract dtaa from database, we hook up our controller to our data context to retrieve them from the database

testing --> cliet--> postman
inject
----------------------------------------------------------------------------------------------------------------------------------------Section 2:

.net sdk comes witha number of different templates so we dotn get started from scratch
basic template- out of the box packages and dependencies


help and contextual help in dotnet cli
dotnet cli is updated alongside sdk

Our project type:
ASP.NET CORE web api, c#
dotnet new webapi command

this projetc is specifically for our web api, runs all of our server side code
try creating 2 distinct projects


Our project relies on authentication (but nothing from existing options)

dotnet new webapi -o DatingApp.API -n DatingApp.API

checkout the out of box stuff with asp.net core

code . ->to open the project in visual studio code

Install extensions if needed

auto complete, syntax highlighting, intellisense, go to definition, find all refernces, debug and support for .net core
ability to create c# classes within solution explorer
nuget package manager- allows us to use VScode to install certain packages we use in our app- nuget packages
angular- npm packages


Program.cs ---> entrypoint into the application, has typically one method main
startup.cs
createwebhostbuilder: go to referce and study them or all the functions in main function 

web servers typically are multithreadedc-ccan handle concurrent e=requets- can handle multiple threads going on at the same time
asynchronous code- thread is not blocked it is open to other requetss, passes of the action of going out
to the database and getting data to a delegate, and when it has result, it continues with the request, it does not
block any of our requests in that thread whilst waiting for result to comeback

----------------------------------------------------------------------------------------------------------------------------------------Section 4:
Angular:

ng new
node modules: packages and dependencies
package.json: identifies the packages that then downloaded inside node modules folder
npm scripts run commands in npm
npm start/ng serve for example to start an angular application
src-->all code e are going to write
app-->compoennets we write live in tbhis folder
default files- starter files- every angular app has to have atleat one app.module file--descorated with ngmodule
app.component.ts-- component.ts--app.module.ts-->
checkout module file--
when moduel is loaded ist going to bootstrap appcomponent file(.ts file)


app compoennt is decorated with component(imported from agular core)
class decorated with component- js class/ts class that has extra features/angular compoent featres

interpolation in standard html
(properties from app component feature class like title)

BootStrap process:
what triggers main.ts file when index.html does not have any javascirp tot typescript 


angular magic: web pack - module bundler- bundle our app into js and same time injects our js into index.html when it builds it

webpack configuration - angular.json not exactly webpack configuration, but angular abstrcting this functionality/coplexity away coz webpack can be difficult to configure

but inside angular.json we have settings that webpack needs to bundle our applucation

start ur application-- starts angular live developmnt server and runs our app: localhost:4200


inspect and the js files you will see are the files bundled by web pack


we write in typescript-->transpiled to js by webpack
https://stackoverflow.com/questions/39246498/compiler-vs-interpreter-vs-transpiler

extensions for angular: angular  by john papa
angular files by Alexander Ivanichev -  to scaffold out componenets
Angular language service - go to definition
angular2 switcher- switch between compoenent files bteween compoennt css and html
auto rename tag
bracket pair colourizer
debugger for chrome
material icon theme
path intellisense - auto completion for file and folder paths
prettier- code formatter
tslint

