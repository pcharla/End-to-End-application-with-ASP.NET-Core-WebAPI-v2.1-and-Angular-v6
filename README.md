# End-to-End-application-with-ASP.NET-Core-WebAPI-v2.1-and-Angular-v6
#Global readme for my revision later
----------------------------------------------------------------------------------------------------------------------------------------
Section 1:
----------------------------------------------------------------------------------------------------------------------------------------
Section 2:
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
----------------------------------------------------------------------------------------------------------------------------------------Section 3:
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

