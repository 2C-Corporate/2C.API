FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["API2C/API2C.csproj", "API2C/"]
RUN dotnet restore "API2C/API2C.csproj"
COPY . .
WORKDIR "/src/API2C"
RUN dotnet build "API2C.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "API2C.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "API2C.dll"]
