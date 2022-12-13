FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["baywatch/baywatch.csproj", "baywatch/"]
RUN dotnet restore "baywatch/baywatch.csproj"
COPY . .
WORKDIR "/src/baywatch"
RUN dotnet build "baywatch.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "baywatch.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "baywatch.dll"]
