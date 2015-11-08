# Live Code for .NET

Live Code is my attempt to build a live coding environment for the development of iOS apps using Xamarin technologies.

It currently works only in Xamarin Studio and only for C#.

## One-time Installation

1. Install the preview version of [Xamarin Inspector](https://developer.xamarin.com/guides/cross-platform/inspector/).

2. Install the Xamarin Studio **Live Code Add-in** from the Gallery in the Add-in Manager.

## Per-app Installation

1. Reference the LiveCode nuget.

2. Put this line of code somewhere in the initialization of your app (`AppDelegate.FinishedLaunching` is a great place):

```csharp
new LiveCode.Server.HttpServer ().Run ();
```

## Running

Run the debug version of your app. It should start as normal.

### Running Snippets

Send snippets of code to be compiled, executed, and visualized using the **Visualize Selection** (Ctrl+Shift+Return) command.

### Live Coding a Class

You can mark a class to be monitored and automatically displayed whenever you edit it (and there are no code errors).

Move your cursor to be within a class and select the **Visualize Class** (Ctrl+Shift+C) command.


## Building

Build the solution `LiveCode.sln`

### Prerequisties

Install the Xamarin Studio **Addin Maker** from the **Addin Development** group in the Gallery.


## How it Works

**Live Code** uses the class [`Mono.CSharp.Evaluator`](http://www.mono-project.com/docs/about-mono/languages/csharp/) to compile and execute code snippets while the app is running.

The IDE add-in allows the user to send snippets to this evaluator. The code is compiled and executed.

If the code produces a value (if it is an expression) then the value is automatically displayed.

The IDE communicates with the device using HTTP on port 9634. Requests and responses are simple JSON bundles.

### Example Request and Response

```bash
$ curl -d "{\"Code\":\"2+2\"}" http://127.0.0.1:9634
```

```json
{"Messages":[],"Duration":"00:00:00.0025132","Result":4,"HasResult":true}
```




