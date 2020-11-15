<p align="center"><img src="assets/collab.svg?raw=true" width="350" alt="Logo"></p>

# WebSockets

[![Build Status](https://dev.azure.com/dimenicsbe/Utilities/_apis/build/status/dimenics.websockets?branchName=master)](https://dev.azure.com/dimenicsbe/Utilities/_build/latest?definitionId=176&branchName=master) ![Azure DevOps coverage](https://img.shields.io/azure-devops/coverage/dimenicsbe/utilities/176)

This is a simple library that can be used to keep track of SignalR connections. This is useful in multi-tenant instances where you don't want to broadcast data to other tenants.

## Getting Started

- You must have Visual Studio 2019 Community or higher.
- The dotnet cli is also highly recommended.

## About this project

This project provides a simple interface and a few implementations for that interface. This makes it configurable and easy to setup in the startup of the application. For example, it requires only 1 line of code to swap an in-memory connection tracker with a SQL connection tracker.

## Build and Test

- Run dotnet restore
- Run dotnet build
- Run dotnet test

## Installation

Use the package manager NuGet to install Dime.Kendo:

`dotnet add package Dime.WebSockets`

## Usage

When a user connects, the connection can be stored in the connection tracker's storage medium. This data can be retrieved when the hub broadcasts data to the clients.

```csharp
public class MyHub : Hub
{
    private readonly IConnectionTracker<Connection> _connectionTracker;

    public MyHub(IConnectionTracker<Connection> connectionTracker)
    {
        _connectionTracker = connectionTracker;
    }

    public override async Task OnConnected()
    {
      await this.ConnectionTracker.AddAsync(new Connection(){ ConnectionId = Context.ConnectionId });
    }
}
```

## Contributing

![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)

Pull requests are welcome. Please check out the contribution and code of conduct guidelines.

## License

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)