# ML.NET CPU Math

This project contains files that handle CPU math operations, whose implementations sometimes involve functions called hardware intrinsics.  It currently supports multi-targeting for both (1) .NET Standard 2.0 and (2) .NET Core App 3.0, each of which follows a separate code path of hardware intrinsics implementations.  When built on .NET Standard 2.0, the project picks up the native implementation.  When built on .NET Core App 3.0, it picks up the managed implemntation.  For those interested in experimenting with this new feature of intrinsics implementations, please read on and follow the following instructions.

## Build the project on .NET Standard 2.0 for native implementations of hardware intrinsics
**Pre-requisite:** On a clean repo, `build.cmd` at the root installs the right version of dotnet.exe and builds the solution. You need to build the solution with native dependencies with `-buildNative`.  The `Release` flag is optional.
``` log
    build.cmd [-Release] -buildNative
```

1. Navigate to the CpuMath directory (machinelearning\src\Microsoft.ML.CpuMath)

2. Build the project with the following command.  The `Release` flag is optional.
``` log
	dotnet build [-c Release] -f netcoreapp2.0
```

**Note:** If you intend to test the performance of intrinsics implementations afterwards, please build in `Release`.

## Build the project on .NET Core App for managed implementations of hardware intrinsics
**Note:** Make sure you have installed the netcoreapp3.0 SDK in the relevant code path (e.g. under `C:\Program Files`).  On a clean repo, `build.cmd` at the root installs the right version of dotnet.exe and builds the solution.  The `Release` flag is optional.
``` log
    build.cmd [-Release]
```

1. Navigate to the CpuMath directory (machinelearning\src\Microsoft.ML.CpuMath)

2. Build the project with the following command.  The `Release` flag is optional.
``` log
	dotnet build [-c Release] -f netcoreapp3.0 /p:UseIntrinsics=true
```

**Note:** If you intend to test the performance of intrinsics implementations afterwards, please build in `Release`.

## Testing correctness: Unit tests for intrinsics implementations
Navigate to the directory for unit tests (machinelearning\test\Microsoft.ML.CpuMath.UnitTests.[TargetFramework: netcoreapp / netstandard]) after building the project for the desired target framework above.

## Testing performance: Performance tests for intrinsics implementations
Navigate to the directory for performance tests (machinelearning\test\Microsoft.ML.CpuMath.PerformanceTests) after building the project for the desired target framework above.