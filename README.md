# MapBox linker issue

1. Created sample MAUI project 

2. Encountered a `clang++` error upon adding **`Mapbox.Maui`** as a NuGet package.

3. Attempted manual referencing of the library after local cloning, still encountering `clang++` error

4. Verbose output from `dotnet build` when package is manually added (from step 3)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fea0d661-4436-40fb-87f5-d4e88ab26620/b3e41127-49c7-42e8-869c-c8c028f9e28b/Untitled.png)

Execution is going well until there is an undefined symbol for `arm64` architecture, see the following errors: 

**** Tried with all supported ABIs (Application Binary interfaces)*

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fea0d661-4436-40fb-87f5-d4e88ab26620/decd712c-80fc-448a-910b-210514b30003/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fea0d661-4436-40fb-87f5-d4e88ab26620/4447b0f7-3716-4f43-bd76-8ec26fcd2f89/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fea0d661-4436-40fb-87f5-d4e88ab26620/ad09c478-b519-4974-9f75-841be7a35729/Untitled.png)

- Target framework is set to `net8.0-android;net8.0-ios` - on both `SampleMaui` & `Mapbox.Maui`
- Tried with all link behaviours: (Do not link, link SDK assemblies only, link everything) - results with the same.

Investigation about the library:

- Latest release version is `10.11.1.1`, last updated 10 months ago
- There is a new alpha version `11.1.0` which is not ready yet, tried the same flow with it but results with the following error: `.nuget/packages/dependencies.gradle/7.6.1/buildTransitive/Dependencies.Gradle.targets(30,3): error GDL001: Gradlew build failed`
    
    Seems like it’s not compatible with .net8.0, `.csproj` still uses `net6.0` 
    
- Manually adding `MapBox 11.1.0` results in missing dependencies because of net6.0