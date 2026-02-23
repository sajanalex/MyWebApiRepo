# Use the .NET 9.0 SDK image (preview or nightly build)
FROM mcr.microsoft.com/dotnet/nightly/sdk:9.0 AS build
WORKDIR /app

# Copy the project file explicitly
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application files
COPY . ./
RUN dotnet publish -c Release -o out

# Use the .NET 9.0 runtime image (preview or nightly build)
FROM mcr.microsoft.com/dotnet/nightly/aspnet:9.0 AS runtime
WORKDIR /app

# Copy the published output from the build stage
COPY --from=build /app/out .

# Expose the port your application runs on
EXPOSE 80

# Set the entry point for the application
ENTRYPOINT ["dotnet", "MyWebApiRepo.dll"]