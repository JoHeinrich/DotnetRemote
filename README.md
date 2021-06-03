# DotnetRemote
Creates interopability between different .net versions and cpu architectures
### Use .net core assembly in .net framework
### Use .net framework assembly in .net core
### Use 32 bit assembly in 64 bit applications
### Use 64 bit assembly in 32 bit applications

## Why?
### Framework vs core
With the discontinuation of .net framework moving to .net core is inevitable.
But not all libraries can easily be migrated.
So how can we move forward while keeping compatibility?

### 32 bit to 64
Your product is still 32 bit and running out of memory
You want to migrate to 64 bit
But there is this one library that only works with 32 bit?

## Solution
Run the program in multiple processes and connect by RPC
But what RPC protokol?
How about one of those legacy protocols?
COM: Allowes for inprocess servers that can connect framework and core. Can be abused for 64 to 32 bit interop.  Only on windows.
WCF: Only for .net framework
GRPC: Only for .net core

Or instead of worrying about RPC calls you can skip all of those worries and just write c#

## Simple to use
### Load Library
```csharp
RemoteFactory factory = new RemoteFactory("path/TestAssembly.dll")
```
### Static calls
```csharp
int result = factory.Execute<int>("TestNamespace.TestClass", "Add", 2, 3);
```
### Dynamic objects
```csharp
dynamic math = factory.Create("TestNamespace.Math");
int result = math.Add(2,3);
```
### Interface oriented
```csharp
IMath math = factory.Create<IMath>("TestNamespace.Math");
int result = math.Add(2,3);
```
### Natural .net events
```csharp
IMath math = factory.Create<IMath>("TestNamespace.Math");
math.OnAddition += x => Console.WriteLine(x);
```


