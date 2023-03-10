# HttUnicorn v0.1.0

[![NuGet](https://img.shields.io/badge/nuget-v0.1.0-blue.svg)](https://www.nuget.org/packages/HttUnicorn/0.0.2-alfa)  

> Designed to help C# programmers creating HTTP Requests, this is The Hypertext Transfer Unicorn :unicorn:

## Usage

### Nuget
You can get **HttpUnicorn** by installing our [NuGet Package](https://www.nuget.org/packages/HttUnicorn/0.1.0);

### Config
**HttUnicorn** uses a config object called UnicornConfig that need a string with the url.

```csharp
var config = new UnicornConfig("http://localhost:3000/todos/");
```

You can also use UnicornConfig to set the Timeout and Headers

```csharp
var config = new UnicornConfig(
  "http://localhost:3000/todos/",
  timeout: new TimeSpan(0, 0, 45),
  headers: new List<UnicornHeader>
  {
    new UnicornHeader("header_name", "header_value"),
    new UnicornHeader("other_header_name", "other_header_value")
  });
```

You can pass the timeout directly as seconds

```csharp
var config = new UnicornConfig(
  "http://localhost:3000/todos/",
  timeoutSeconds: 35
  );
```

You can start following the examples bellow:

### Get

```csharp
List<Todo> todos = await new Unicorn(config).GetModelAsync<List<Todo>>();

string todosString = await new Unicorn(config).GetStringAsync();

using(HttpResponseMessage responseMessage = 
  await new Unicorn(config).GetResponsegAsync())
{
    //deal with the response message
}
```

### Post

```csharp
Todo generatedTodo = await new Unicorn(config)
  .PostModelAsync<Todo, Todo>(new Todo
  {
    Completed = true,
    Title = "todo",
    UserId = 36
  });
```
```csharp
string stringResponseBody = await new Unicorn(config)
  .PostStringAsync(new Todo
  {
    Completed = true,
    Title = "todo",
    UserId = 36
  });
```

```csharp
using(HttpResponseMessage responseMessage = 
  await new Unicorn(config).PostResponsegAsync())
{
    //deal with the response message
}
```

### Put

```csharp
Todo updatedTodo = await new Unicorn(config)
                    .PutModelAsync<Todo, Todo>(todo);
```

### Delete

```csharp
MyApiResponse response = await new new Unicorn(config)
                          .DeleteModelAsync<MyApiResponse>(key);
//This one is for situations when the requested API returns an object in the body of the response.
---


