FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["calc/calc.csproj", "calc/"]
RUN dotnet restore "calc/calc.csproj"
COPY . .
WORKDIR "/src/calc"
RUN dotnet build "calc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "calc.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "calc.dll"]
