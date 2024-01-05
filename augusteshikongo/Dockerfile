#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["augusteshikongo.github.io/augusteshikongo/augusteshikongo.csproj", "augusteshikongo.github.io/augusteshikongo/"]
RUN dotnet restore "./augusteshikongo.github.io/augusteshikongo/./augusteshikongo.csproj"
COPY . .
WORKDIR "/src/augusteshikongo.github.io/augusteshikongo"
RUN dotnet build "./augusteshikongo.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./augusteshikongo.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "augusteshikongo.dll"]