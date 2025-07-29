ARG DOTNET_VERSION=8.0

# --- Build Stage ---
FROM mcr.microsoft.com/dotnet/sdk:${DOTNET_VERSION} AS build
WORKDIR /app

# Copy everything and restore
COPY . . 
RUN dotnet restore

# Publish the app
RUN dotnet publish -c Release -o /publish

# --- Runtime Stage ---
FROM mcr.microsoft.com/dotnet/aspnet:${DOTNET_VERSION} AS runtime
WORKDIR /app
COPY --from=build /publish .

# Expose port (Azure listens on 80)
EXPOSE 80

ENTRYPOINT ["dotnet", "WebApplication1.dll"]
