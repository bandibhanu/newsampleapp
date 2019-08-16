FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["sampledockerapp/sampledockerapp.csproj", "sampledockerapp/"]
RUN dotnet restore "sampledockerapp/sampledockerapp.csproj"
COPY . .
WORKDIR "/src/sampledockerapp"
RUN dotnet build "sampledockerapp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "sampledockerapp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "sampledockerapp.dll"]
