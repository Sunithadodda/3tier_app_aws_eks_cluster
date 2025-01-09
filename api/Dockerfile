# Use the official .NET SDK image for building the application
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

# Set the working directory for the build
WORKDIR /src

# Copy the .csproj file and restore dependencies
COPY ["Basic3TierAPI/Basic3TierAPI.csproj", "Basic3TierAPI/"]

# Restore the dependencies
RUN dotnet restore "Basic3TierAPI/Basic3TierAPI.csproj"

# Copy the rest of the application code
COPY . .

# Set the working directory to the app folder and build the application
WORKDIR "/src/Basic3TierAPI"
RUN dotnet build -c Release -o /app/build

# Publish the application
RUN dotnet publish -c Release -o /app/publish

# Use the official .NET Runtime image for running the application
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base

# Set the working directory for the final image
WORKDIR /app

# Expose the necessary ports
EXPOSE 80
EXPOSE 443

# Copy the published output from the build stage
COPY --from=build /app/publish .

# Define the entry point for the application
ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]
