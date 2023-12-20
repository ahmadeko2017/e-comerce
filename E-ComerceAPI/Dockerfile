FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["E-ComerceAPI/E-ComerceAPI.csproj", "E-ComerceAPI/"]
RUN dotnet restore "E-ComerceAPI/E-ComerceAPI.csproj"
COPY . .
WORKDIR "/src/E-ComerceAPI"
RUN dotnet build "E-ComerceAPI.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "E-ComerceAPI.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "E-ComerceAPI.dll"]
