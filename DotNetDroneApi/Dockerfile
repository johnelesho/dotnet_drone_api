FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DotNetDroneApi/DotNetDroneApi.csproj", "DotNetDroneApi/"]
RUN dotnet restore "DotNetDroneApi/DotNetDroneApi.csproj"
COPY . .
WORKDIR "/src/DotNetDroneApi"
RUN dotnet build "DotNetDroneApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNetDroneApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetDroneApi.dll"]
