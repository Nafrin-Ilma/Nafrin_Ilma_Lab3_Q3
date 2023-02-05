#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["MyCoreApp_301156573/MyCoreApp_301156573.csproj", "MyCoreApp_301156573/"]
RUN dotnet restore "MyCoreApp_301156573/MyCoreApp_301156573.csproj"
COPY . .
WORKDIR "/src/MyCoreApp_301156573"
RUN dotnet build "MyCoreApp_301156573.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyCoreApp_301156573.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyCoreApp_301156573.dll"]
