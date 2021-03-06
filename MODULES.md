![DropCore GitHub Header](https://raw.githubusercontent.com/dropcore/image-assets/master/github-header.png)

# Modules

This document details how modules are implemented.

## Structure

Below is an example of how a module would be structure. You might also take a look at `DropCore.Module.User` and the related class libraries.

### DropCore.Module.Example

**Type:** `Class Library`

This project contains the main web-application part of the module. That would include any controllers, view models or views.

#### Required packages

* `Microsoft.AspNet.Mvc`
* `MvcCodeRouting`
* `Unity`

### DropCore.Module.Example.Shared

**Type:** `Class Library`

This project contains any re-usable logic for the module that might be shared to any other module that wants to take advantage of the functionality provided by the module.

This would include any data models, repositories or services.

#### Required packages

* `Dapper`

### DropCore.Module.Example.Schema

**Type:** `Class Library`

This project contains all migration logic for the database portion of the module. This includes migration of tables as well as seeding of test data for unit tests.

#### Required packages

* `FluentMigrator`

### DropCore.Module.Example.Tests

**Type:** `Unit Test Project`

This project contains the unit tests for all implemented functionality of the module.

## Quirks

### Razor views

Due to how **Visual Studio** works internally to provide functionality for **Razor**, you must take a few actions in order to get **Razor** views working for your module project.

#### Syntax highlighting

##### Symptom

    @model DropCore.Module.Example.Shared.Models.Example
    
    The name 'model' does not exist in the current context

##### Solution

Copy `DropCore.App\Views\web.config` into the `Views\` folder of your module project.

#### Intellisense

##### Symptom

    <h3>Hello, @Model.Name</h3>
    
    The name 'Model' does not exist in the current context

##### Solution

Change the `Output path` of your module project from `bin\Debug` and `bin\Release` to `bin\`.
