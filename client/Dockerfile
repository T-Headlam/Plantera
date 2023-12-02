# Stage 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the project file and restore dependencies
COPY client.csproj .
RUN dotnet restore

# Copy the remaining source code and build the app
COPY . .
RUN dotnet build -c Release -o /app

# Stage 2: Publish the application
FROM build AS publish
RUN dotnet publish -c Release -o /app

# Stage 3: Create the final image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy the published application from the publish stage
COPY --from=publish /app .

# Expose port 80 for the Blazor Server app
EXPOSE 80

# Entry point to run the application
ENTRYPOINT ["dotnet", "client.dll"]
